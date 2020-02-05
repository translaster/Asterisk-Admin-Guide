# Fundamentals

## Asterisk Architecture
From an architectural standpoint, Asterisk is made up of many different modules. This modularity gives you an almost unlimited amount of flexibility in the design of an Asterisk-based system. As an Asterisk administrator, you have the choice on which modules to load and the configuration of each module. Each module that you load provides different capabilities to the system. For example, one module might allow your Asterisk system to communicate with analog phone lines, while another might add call reporting capabilities. In this section, we'll discuss the overall relationships of some Asterisk component, the various types of modules and their capabilities.

## Directory and File Structure

## Asterisk Configuration

The top-level page for all things related to Asterisk configuration

## Asterisk Internal Database

Asterisk comes with a database that is used internally and made available for Asterisk programmers and administrators to use as they see fit.

Asterisk versions up to 1.8 used the Berkeley DB, and in version 10 the project moved to the SQLite3 database. You can read about database migration between those major versions in the section SQLite3 astdb back-end.

## Key Concepts

Under Construction

Top-level page for a section dealing with concepts of the key moving pieces in Asterisk that an **administrator** needs to understand. Channels,
Bridges, Frames, etc.

### States and Presence

Asterisk includes the concepts of Device State , Extension State and Presence State which together allow Asterisk applications and interfaces to
receive information about the state of devices, extensions and the users of the devices.

As an example, channel drivers like chan_sip or res_pjsip/chan_pjsip may both provide devices with device state, plus allow devices to subscri
be to hints to receive notifications of state change. Other examples would be app_queue which takes into consideration the device state of
queue members to influence queue logic or the Asterisk Manager Interface which provides actions for querying extension state and presence state.

Additionally, modules exist for Corosync and XMPP PubSub support to allow device state to be shared and distributed across multiple systems.
The sub-sections here describe these concepts, point to related module specific configuration sections and discuss Querying and Manipulating State in
formation.
The figure below may help you get an idea of the overall use of states and presence with the Asterisk system. It has been simplified to focus on the
flow and usage of state and presence. In reality, the architecture can be a bit more confusing. For example a module could both provide subscription
functionality for a subscriber and be the same module providing the devices and device state on the other end.

![](/pics/states_1.png)

#### Device State

##### Devices

Devices are discrete components of functionality within Asterisk that serve a particular task. A device may be a channel technology resource, such as SIP/<name> in the case of chan_sip.so or a feature resource of another module such as app_confbridge.so which provides devices like confbridge:<name>.

###### State information

Asterisk devices make state information available to the Asterisk user, such that a user might make use of the information to affect call flow or behavior of the Asterisk system. The device state identifier for a particular device is typically very similar to the device name. For example the device state identifier for SIP/6001 would be SIP/6001, for confbridge 7777 it would be confbridge:7777. Device states have a one-to-one mapping to the device they represent. That is opposed to other state providers in Asterisk which may have one-to-many relationships, such as Extension State.
The Querying and Manipulating State section covers how to access or manipulate device state as well as other states.

##### Common Device State Providers

Device state providers are the components of Asterisk that provide some state information for their resources. The device state providers available in Asterisk will depend on the version of Asterisk you are using, what modules you have installed and how those modules are configured. Here is a list of the common device state identifiers you will see and what Asterisk component provides the resources and state.

| Device State Identifier | Device State Provider |
| :---------------------- | :-------------------- |
| PJSIP/<resource> | PJSIP SIP stack, res_pjsip.so, chan_pjsip.so. |
| SIP/<resource> | The older SIP channel driver, chan_sip.so. |
| DAHDI/<resource> | The popular telephony hardware interface driver, chan_dahdi.so. |
| IAX2/<resource> | Inter-Asterisk Exchange protocol! chan_iax2.so. |
| ConfBridge:<resource> | The conference bridge application, app_confbridge.so. |
| MeetMe:<resource> | The older conference bridging app, app_meetme.so. |
| Park:<resource> | The Asterisk core in versions up to 11. res_parking.so in versions 12 or greater. |
| Calendar:<resource> | res_calendar.so and related calendaring modules. |
| Custom:<resource> | Custom device state provided by the asterisk core. |

Note that we are not differentiating any device state providers based on what is on the far end. Depending on device state provider, the far end of signaling for state could be a physical device, or just a discrete feature resource inside of Asterisk.  In terms of understanding device state for use in Asterisk, it doesn't really matter. The device state represents the state of the Asterisk device as long as it is able to provide it regardless of what is on the far end of the communication path.

###### Custom Device States

The Asterisk core provides a Custom device state provider (custom:<resource>) that allows you to define arbitrary device state resources. See the Querying and Manipulating State section for more on using custom device state.

##### Possible Device States

Here are the possible states that a device state may have.

* UNKNOWN
* NOT_INUSE
* INUSE
* BUSY
* INVALID
* UNAVAILABLE
* RINGING
* RINGINUSE
* ONHOLD

Though the label for each state carries a certain connotation, the actual meaning of each state is really up to the device state provider. That is, any particular state may mean something different across device state providers.

##### Module Specific Device State

There is module specific configuration that you must be aware of to get optimal behavior with certain state providers.

For chan_sip see the chan_sip State and Presence Options section.

For res_pjsip see the Configuring res_pjsip for Presence Subscriptions section.

#### Extension State and Hints

##### Overview

Extension state is the state of an Asterisk extension, as opposed to the direct state of a device or a user. It is the aggregate of Device state from devices mapped to the extension through a hint directive. See the States and Presence section for a diagram showing the relationship of all the various states.

Asterisk's SIP channel drivers provide facilities to allow SIP presence subscriptions (RFC3856) to extensions with a defined hint. With an active subscription, devices can receive notification of state changes for the subscribed to extension. That notification will take the form of a SIP NOTIFY with PIDF content (RFC3863) containing the presence/state information.

##### Defining Hints

For Asterisk to store and provide state for an extension, you must first define a hint for that extension. Hints are defined in the Asterisk dialplan, i.e. extensions.conf.

When Asterisk loads the configuration file it will create hints in memory for each hint defined in the dialplan. Those hints can then be queried or manipulated by functions and CLI commands. The state of each hint will regularly be updated based on state changes for any devices mapped to a hint.

The full syntax for a hint is

```
exten = <extension>,hint,<device state id>[& <more dev state id],<presence state id>
```

Here is what you might see for a few configured hints.

```
[internal]
exten = 6001,hint,SIP/Alice&SIP/Alice-mobile
exten = 6002,hint,SIP/Bob
exten = 6003,hint,SIP/Charlie&DAHDI/3
exten = 6004,hint,SIP/Diane,CustomPresence:Diane
exten = 6005,hint,,CustomPresence:Ellen
```

Things of note:

* You may notice that the syntax for a hint is similar to a regular extension, except you use the hint keyword in place of the priority. Remember these special hint directives are used at load-time and not during run-time, so there is no need for a priority.
* Multiple devices can be mapped to an extension by providing an ampersand delimited list.
* A presence state ID is set after the device state IDs. If set with only a presence state provider you must be sure to include a blank field after the hint as in the example for extension 6005.
* Hints can be anywhere in the dialplan. Though, remember that dialplan referencing the extension and devices subscribing to it will need use the extension number/name and context. The hints shown above would be 6001@internal, 6002@internal, etc, just like regular extensions.

#### Querying Extension State

The Querying and Manipulating State section covers accessing and affecting the various types of state.

For a quick CLI example, once you have defined some hints, you can easily check from the CLI to verify they get loaded correctly.

```
*CLI> core show hints
-= Registered Asterisk Dial Plan Hints =-
6003@internal : SIP/Charlie&DAHDI/3 State:Unavailable Watchers 0
6002@internal : SIP/Bob State:Unavailable Watchers 0
6001@internal : SIP/Alice&SIP/Alice- State:Unavailable Watchers 0
6005@internal : ,CustomPresence:Elle State:Unavailable Watchers 0
6004@internal : SIP/Diane,CustomPres State:Unavailable Watchers 0
----------------
- 5 hints registered
```

In this example I was lazy, so they don't have real providers mapped otherwise you would see various states represented.

##### SIP-подписка на Asterisk hints

После настройки подсказки драйверы SIP Asterisk можно настроить так, чтобы разрешить агентам пользователей SIP подписываться на подсказки. Подписка приведет к отправке подписчику уведомлений об изменении состояния.

Конфигурация для chan_sip обсуждается в разделе Настройка chan_sip для подписок на присутствие

Настройка res_pjsip обсуждается в разделе [Настройка res_pjsip для подписок на присутствие](configuration.md#настройка-res_pjsip-для-подписок-на-присутствие)

#### Состояние присутствия

##### Обзор

Asterisk 11 был оснащен поддержкой состояний присутствия. Простой способ понять это - сравнить поддержку состояния присутствия с поддержкой состояния устройства, которая всегда была у Asterisk. Как и в случае с поддержкой состояния устройства, Asterisk имеет базовый API, позволяющий модулям регистрироваться в качестве поставщиков состояния присутствия, оповещать других об изменениях состояния присутствия и запрашивать состояние присутствия других. Различие между понятиями устройства и состояния присутствия становится ясным благодаря пониманию субъекта состояния для каждого понятия.

* Состояние устройства отражает текущее **состояние физического устройства**, подключенного к Asterisk.
* Состояние присутствия отражает текущее **состояние пользователя** устройства .

Например, **устройство** может в данный момент не использоваться (состояние `not in use`), но **человек** отсутствует (`away`). Это может быть важной деталью при определении доступности **человека**.

Хотя архитектуры поддержки состояния присутствия и состояния устройства в Asterisk схожи, между ними есть некоторые ключевые различия.

* Asterisk не может сделать вывод об изменениях состояния присутствия так же, как и об изменениях состояния устройства. Например, когда конечная точка SIP находится в состоянии вызова, Asterisk может сделать вывод, что устройство используется, и сообщить о состоянии устройства как о используемом (`in use`). Однако Asterisk не может определить, не хочет ли пользователь такого устройства, чтобы его беспокоили, или предпочитает общаться в чате. Таким образом, все изменения состояния присутствия должны выполняться вручную.
* Asterisk не учитывает присутствие при определении доступности устройства. Например, участники очереди, состояние устройства которых `busy`, не будут вызваны; однако, если устройство этого участника `not in use`, но его присутствие `away`, Asterisk все равно попытается вызвать этого участника очереди.
* Asterisk не может объединить несколько состояний присутствия в одно объединенное состояние. Несколько состояний устройства могут быть перечислены в приоритете подсказки (hint) расширения, чтобы иметь отчет о комбинированном состоянии. Наличие поддержки состояния в Asterisk лишено этой концепции.

##### Состояния присутствия

* `not_set`: для этой сущности не задано состояние присутствия.
* `unavailable`: этот объект присутствует, но в настоящее время недоступен для связи.
* `available`: эта сущность доступна для связи.
* `away`: эта сущность отсутствует и не может общаться.
* `xa`: эта сущность отсутствует и, как ожидается, не вернется в течение некоторого времени.
* `chat`: эта сущность доступна для общения, но предпочитает использовать мгновенные сообщения, а не говорить.
* `dnd`: эта сущность не желает, чтобы ее беспокоили.

##### Подтип и сообщение

В дополнение к основным состояниям присутствия, представленным, присутствие также имеет понятие **подтипа** и **сообщения**.

Подтип - это краткий метод описания природы состояния. Например, подтип для статуса `away` может быть "at home".

Сообщение представляет собой более длинное объяснение текущего состояния присутствия. Используя тот же пример из прошлого, сообщение может быть "Болен гриппом. Ушел до 18-го".

##### func_presencestate And The CustomPresence Provider

Единственным поставщиком состояния присутствия в Asterisk 11 является поставщик `CustomPresence`. Этот поставщик ппредоставляется модулем `func_presencestate.so`, предоставляющим доступ к функции диалплана `PRESENCE_STATE`. Документацию по `PRESENCE_STATE` можно найти [здесь](https://wiki.asterisk.org/wiki/display/AST/Asterisk+11+Function_PRESENCE_STATE). `CustomPresence` не зависит от устройства в ядре и может быть удобным способом установить и запросить присутствие из диалплана или API, таких как AMI.

Простой пример использования `CustomPresence` в диалплане показан ниже.

```
[default]
exten => 2000,1,Answer()
same => n,Set(CURRENT_PRESENCE=${PRESENCE_STATE(CustomPresence:Bob,value)})
same => n,GotoIf($[${CURRENT_PRESENCE}=available]?set_unavailable:set_available)
same => n(set_available),Set(PRESENCE_STATE(CustomPresence:Bob)=available,,)
same => n,Goto(finished)
same => n(set_unavailable),Set(PRESENCE_STATE(CustomPresence:Bob)=unavailable,,)
same => n(finished),Playback(queue-thankyou)
same => n,Hangup
exten => 2001,1,GotoIf($[${PRESENCE_STATE(CustomPresence:Bob,value)}!=available]?voicemail)
same => n,Dial(SIP/Bob)
same => n(voicemail)VoiceMail(Bob@default)
```

С помощью этого диалплана пользователь может набрать `2000@default` для переключения присутствия Боба между `available` и `unavailable`. Когда пользователь пытается позвонить Бобу, используя `2001@default`, если присутствие Боба в данный момент `unavailable`, то вызов будет отправлен непосредственно на голосовую почту.

---
Одна вещь, которую следует иметь в виду с функцией диалплана `PRESENCE_STATE`, состоит в том, что, как и с `DEVICE_STATE`, состояние может быть запрошено у любого поставщика присутствия, но `PRESENCE_STATE` способен только устанавливать состояние присутствия для поставщика состояния присутствия `CustomPresence`.
---

##### Настройка подписки на присутствие с хинтами

Как уже упоминалось в разделе поддержки телефона, на момент написания статьи это будет работать только с телефонами Digium.

Как и в случае с состоянием устройства, состояние присутствия связывается с расширением диалплана с помощью хинта (подсказки). Хинты состояния присутствия следуют за состоянием устройства в расширении хинта и разделяются запятой (,). В качестве примера:

```
[default]
exten => 2000,hint,SIP/2000,CustomPresence:2000
exten => 2000,1,Dial(SIP/2000)
same => n,Hangup()
```

Или же можно определить поставщика состояния присутствия без устройства.

```
exten => 2000,hint,,CustomPresence:2000
```

**Первый** пример позволит пользователю, подписавшемуся на состояние расширения `2000@default`, получать уведомления об изменениях состояния устройства для устройства `SIP/2000`, а также изменения состояния присутствия для поставщика присутствия `CustomPresence:2000`.

**Второй** пример позволит абоненту получать уведомления об изменениях состояния только для поставщика присутствия `CustomPresence:2000`.

Поставщик состояния присутствия `CustomPresence` будет обсуждаться далее на этой странице.

Также, как и в случае с состоянием устройства, существует команда AMI для запроса состояния присутствия. Документацию по команде AMI PresenceState можно найти [здесь](https://wiki.asterisk.org/wiki/display/AST/Asterisk+11+ManagerAction_PresenceState).

##### Example Presence Notification

When a SIP device is subscribed to a hint you have configured in Asterisk and that hint references a presence state provider, then upon change of that state Asterisk will generate a notification. That notification will take the form of a SIP NOTIFY including XML content. In the expanding panel below I've included an example of a presence notification sent to a Digium phone. This particular presence notification happened when we changed presence state for CustomPresence:6002 via the CLI command 'presencestate change'.

```
myserver*CLI> presencestate change CustomPresence:6002 UNAVAILABLE
Changing 6002 to UNAVAILABLE
set_destination: Parsing <sip:6002@10.24.18.138:5060;ob> for address/port to send to
set_destination: set destination to 10.24.18.138:5060
Reliably Transmitting (no NAT) to 10.24.18.138:5060:
NOTIFY sip:6002@10.24.18.138:5060;ob SIP/2.0
Via: SIP/2.0/UDP 10.24.18.124:5060;branch=z9hG4bK68008251;rport
Max-Forwards: 70
From: sip:6002@10.24.18.124;tag=as722c69ec
To: "Bob" <sip:6002@10.24.18.124>;tag=4DpRZfRIlaKU9iQcaME2APx85TgFOEN7
Contact: <sip:6002@10.24.18.124:5060>
Call-ID: JVoQfeZe1cWTdPI5aTWkRpdqkjs8zmME
CSeq: 104 NOTIFY
User-Agent: Asterisk PBX SVN-branch-12-r413487
Subscription-State: active
Event: presence
Content-Type: application/pidf+xml
Content-Length: 602
<?xml version="1.0" encoding="ISO-8859-1"?>
<presence xmlns="urn:ietf:params:xml:ns:pidf"
xmlns:pp="urn:ietf:params:xml:ns:pidf:person"
xmlns:es="urn:ietf:params:xml:ns:pidf:rpid:status:rpid-status"
xmlns:ep="urn:ietf:params:xml:ns:pidf:rpid:rpid-person"
entity="sip:6002@10.24.18.124">
<pp:person><status>
</status></pp:person>
<note>Ready</note>
<tuple id="6002">
<contact priority="1">sip:6002@10.24.18.124</contact>
<status><basic>open</basic></status>
</tuple>
<tuple id="digium-presence">
<status>
<digium_presence type="unavailable" subtype=""></digium_presence>
</status>
</tuple>
</presence>
---
== Extension Changed 6002[from-internal] new state Idle for Notify User 6002
<--- SIP read from UDP:10.24.18.138:5060 --->
SIP/2.0 200 OK
Via: SIP/2.0/UDP 10.24.18.124:5060;rport=5060;received=10.24.18.124;branch=z9hG4bK68008251
Call-ID: JVoQfeZe1cWTdPI5aTWkRpdqkjs8zmME
From: <sip:6002@10.24.18.124>;tag=as722c69ec
To: "Bob" <sip:6002@10.24.18.124>;tag=4DpRZfRIlaKU9iQcaME2APx85TgFOEN7
CSeq: 104 NOTIFY
Contact: "Bob" <sip:6002@10.24.18.138:5060;ob>
Allow: PRACK, INVITE, ACK, BYE, CANCEL, UPDATE, SUBSCRIBE, NOTIFY, REFER, MESSAGE, OPTIONS
Supported: replaces, 100rel, timer, norefersub
Content-Length: 0
<------------->
```

##### Phone Support for Presence State via SIP presence notifications

At the time of writing, only Digium phones have built-in support for interpreting Asterisk's Presence State notifications (as opposed to SIP presence notifications for extension/device state). The CustomPresence provider itself is device-agnostic and support for other devices could be added in. Or devices themselves (soft-phone or hardphone) could be modified to interpret the XML send out in the Presence State notification.

##### Digium Phones

This Video provides more insight on how presence can be set and viewed on Digium phones.

When using Digium phones with the Digium Phone Module for Asterisk, you can set hints in Asterisk so that when one Digium phone's presence is updated, other Digium phones can be notified of the presence change. The DPMA automatically creates provisions such that when a Digium Phone updates its presence, CustomPresence:<line name> is updated, where <line name> is the value set for the line= option in a type=phone category. Using the example dialplan from the Overview section, Digium phones that are subscribed to 2000@default will automatically be updated about line 2000's presence whenever line 2000's presence changes.

---
Digium phones support only the available, away, dnd, xa, and chat states. The unavailable and not_set states are not supported.
---

#### Querying and Manipulating State

##### Overview

This section will enumerate and briefly describe the ways in which you can query or manipulate the various Asterisk state resources. Device State, Extension State and Presence State. Where mentioned, the various functions and commands will be linked to further available documentation.

##### Device State

The DEVICE_STATE function will return the Device State for a specified device state identifier and allow you to set Custom device states.

On the command line, the devstate command will allow you to list or modify Custom device states specifically.

```
devstate change -- Change a custom device state
devstate list -- List currently known custom device states
```

##### Extension State

The EXTENSION_STATE function will return the Extension State for any specified extension that has a defined hint.

The CLI command core show hints will show extension state for all defined hints, as well as display a truncated list of the mapped Device State or
Presence State identifiers.

```
myserver*CLI> core show hints
-= Registered Asterisk Dial Plan Hints =-
6002@from-internal : SIP/6002 State:Unavailable Watchers 0
7777@from-internal : SIP/6003,CustomPrese State:Unavailable Watchers 0
----------------
- 2 hints registered
```

##### Presence State
Added in Asterisk 11, the PRESENCE_STATE function will return Presence State for any specified Presence State identifier, or set the Presence State for specifically for a CustomPresence identifier.

The presencestate CLI command will list or modify any currently defined Presence State resources provided by the CustomPresence provider.

```
myserver*CLI> core show help presencestate
presencestate change -- Change a custom presence state
presencestate list -- List currently know custom presence states
```

##### Asterisk Manager Interface actions

Any of the previously mentioned functions could be called via AMI with the Setvar and Getvar actions.

Then there are two more specific actions called ExtensionState and PresenceState. See the linked documentation for more info.
