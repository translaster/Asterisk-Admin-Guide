# Configuration

Этот раздел содержит множество подразделов, посвященных настройке каждого аспекта Asterisk. Помимо того, что описано в разделе [Core Configuration](#core-configuration), большинство особенностей и функций предоставляются модулями, которые могут быть установлены или не установлены в системе Asterisk. Встроенная документация по конфигурации для каждого модуля (который имеет документацию) может быть доступна через [CLI Asterisk](operation.md#asterisk-command-line-interface). В разделе [CLI Syntax and Help Commands](operation.md#cli-syntax-and-help-commands) содержатся дополнительные сведения о доступе к справке по конфигурации модуля.

## Core Configuration

The sub-pages here cover any possible configuration of Asterisk's core. That is, functionality which is not separated out into modules.
If you are unfamiliar with the core and modules concepts, take a look at the Asterisk Architecture section.

## Channel Drivers

Все об Asterisk и драйверах каналов

### SIP

Раздел в разработке

Раздел для хранения информации о настройке драйверов каналов SIP: chan_sip и chan_pjsip

#### Configuring chan_sip

Раздел в разработке - страница не завершена!

В настоящее время документация находится в файле sip.conf.sample и прилагается к исходникам. Мы находимся в процессе обновления Вики!

##### chan_sip State and Presence Options

###### Device State

Существует несколько вариантов конфигурации chan_sip, которые влияют на поведение состояния устройства.

**callcounter**

The **callcounter** option in sip.conf **must be enabled** for SIP devices (e.g. SIP/Alice) to provide advanced device state. Without it you may see some state, such as unavailable or idle, but not much more.

The option can be set in the general context, or on a per-peer basis.

Default: no

```
[general]
callcounter=yes
```

**busylevel**

The **busylevel** option only works if call counters are enabled via the above option. If call counters are enabled, then busylevel allows you to set a threshold for when to consider this device busy. If busylevel is set to 2, then only at 2 or more calls will the device state report BUSY. The busylevel option can only be set for peers.
Default: 0

```
[6001]
type=friend
busylevel=2
```

**notifyhold**

The **notifyhold** option, when enabled, adds the ONHOLD device state to the range of possible device states that chan_sip will use.

This option can only be set in the general section.

Default: yes

```
[general]
notifyhold=no
```

##### Extension State, Hints, Subscriptions
Extension State and subscriptions tend to go hand in hand. That is, if you are using Extension State, you probably have SIP user agents subscribing to
those extensions/hints. These options all affect that behavior.

**allowsubscribe**

The **allowsubscribe** option enables or disables support for any kind of subscriptions. You can set allowsubscribe per-peer or in the general section.

Default: yes

```
[6001]
type=friend
allowsubscribe=no
```

**subscribecontext**

**subscribecontext** sets a specific context to be used for subscriptions. That means, if SIP user agent subscribes to this peer, Asterisk will search for an associated hint mapping in the context specified.

This option can be set per-peer or in the general section.

Default: null (by default Asterisk will use the context specified with the "context" option)

```
[6001]
type=friend
context=internal
subscribecontext=myhints
```

**notifyringing**
**notifyringing** enables or disables notifications for the RINGING state when an extension is already INUSE. Only affects subscriptions using the dialog-inf o event package. Option can be configured in the general section only. It cannot be set per-peer.

Default: yes

```
[general]
notifyringing=no
```

**notifycid**
**notifycid** some nuance and may only be relevant to SNOM phones or others that support dialog-info+xml notifications. Below are the notes from the
sample sip.conf.

Default: no

```
;notifycid = yes    ; Control whether caller ID information is sent along with
                    ; dialog-info+xml notifications (supported by snom phones).
                    ; Note that this feature will only work properly when the
                    ; incoming call is using the same extension and context that
                    ; is being used as the hint for the called extension. This means
                    ; that it won't work when using subscribecontext for your sip
                    ; user or peer (if subscribecontext is different than context).
                    ; This is also limited to a single caller, meaning that if an
                    ; extension is ringing because multiple calls are incoming,
                    ; only one will be used as the source of caller ID. Specify
                    ; 'ignore-context' to ignore the called context when looking
                    ; for the caller's channel. The default value is 'no.' Setting
                    ; notifycid to 'ignore-context' also causes call-pickups attempted
                    ; via SNOM's NOTIFY mechanism to set the context for the call pickup
                    ; to PICKUPMARK.
```

##### Configuring chan_sip for IPv6

##### Обмен состоянием устройств и почтового ящика с помощью PJSIP

###### Фон

Asterisk разрешил обмен состоянием устройства и почтового ящика для многих версий. Обычно это делается с помощью модуля res_xmpp для экземпляров в разных сетях или с помощью res_corosync для экземпляров в одной сети. Это потребовало в некоторых случаях чрезвычайно большого объема работы по настройке. В случае res_xmpp это также добавляет еще одну точку отказа для обмена в виде самого сервера XMPP. С другой стороны, модуль res_pjsip_publish_asterisk этим не страдает.

###### Функционирование

Модуль res_pjsip_publish_asterisk устанавливает необязательную двунаправленную или однонаправленную связь между экземплярами Asterisk. При изменении состояния устройства или почтового ящика на одном экземпляре Asterisk - оно отправляется на другой экземпляр Asterisk с помощью сообщения PUBLISH, содержащего конкретное тело Asterisk. Это тело состоит из JSON и содержит информацию, необходимую для отражения изменения удаленного состояния. Для ситуаций, когда вы не хотите предоставлять доступ ко всем состояниям или не хотите разрешать получение всех состояний, вы можете дополнительно отфильтровать их с помощью регулярного выражения. Это ограничивает объем трафика.

###### Конфигурация

Конфигурирование вещей для обмена состояниями требует нескольких различных объектов: endpoint, publish, asterisk-publication и необязательно auth. Все они настраивают определенную часть в обмене. Конечная точка должна быть настроена как фундаментальная часть PJSIP, так как **все** входящие запросы связаны с конечной точкой. Объект publish сообщает res_pjsip_outbound_publish куда отправлять PUBLISH и какой тип сообщения PUBLISH отправлять. Объект asterisk-publication конфигурирует обработку сообщений PUBLISH, включая то, разрешены ли они и от кого. Наконец, вы можете по желанию использовать auth, чтобы сообщения PUBLISH подвергались проверке для учетных данных.

###### Пример конфигурации

Приведенная ниже конфигурация предназначена для двух экземпляров Asterisk, совместно использующих все состояния устройства и почтового ящика между ними.

Экземпляр №1 (IP-адрес: 172.16.10.1):

```
[instance2]
type=endpoint

[instance2-devicestate]
type=outbound-publish
server_uri=sip:instance1@172.16.10.2
event=asterisk-devicestate

[instance2-mwi]
type=outbound-publish
server_uri=sip:instance1@172.16.10.2
event=asterisk-mwi

[instance2]
type=inbound-publication
event_asterisk-devicestate=instance2
event_asterisk-mwi=instance2

[instance2]
type=asterisk-publication
devicestate_publish=instance2-devicestate
mailboxstate_publish=instance2-mwi
device_state=yes
mailbox_state=yes
```

Это настраивает первый экземпляр для публикации состояния устройства и почтового ящика в 'instance2', расположенный по адресу 172.16.10.2, с использованием имени ресурса 'instance1' без аутентификации. Поскольку фильтры отсутствуют - все состояния будут опубликованы. Он также настраивает первый экземпляр на прием всех сообщений о состоянии устройства и почтового ящика, опубликованных для ресурса с именем 'instance2' из 'instance2'.

Экземпляр № 2 (IP-адрес: 172.16.10.2):

```
[instance1]
type=endpoint

[instance1-devicestate]
type=outbound-publish
server_uri=sip:instance2@172.16.10.1
event=asterisk-devicestate

[instance1-mwi]
type=outbound-publish
server_uri=sip:instance2@172.16.10.1
event=asterisk-mwi

[instance1]
type=inbound-publication
event_asterisk-devicestate=instance1
event_asterisk-mwi=instance1

[instance1]
type=asterisk-publication
devicestate_publish=instance1-devicestate
mailboxstate_publish=instance1-mwi
device_state=yes
mailbox_state=yes
```

Это настраивает второй экземпляр на публикацию состояний устройств и почтового ящика в 'instance1', расположенный по адресу 172.16.10.1, с использованием имени ресурса 'instance2' без аутентификации. Поскольку фильтры не существуют - все состояния будут опубликованы. Он также настраивает второй экземпляр на прием всех сообщений о состоянии устройства и почтового ящика, опубликованных для ресурса с именем 'instance1' из 'instance1'.

###### Фильтрация

Как уже упоминалось - события состояния могут быть отфильтрованы устройством или почтовым ящиком, к которым они относятся с помощью регулярного выражения. Это настраивается для типов 'publish' с использованием '@device_state_filter' и '@mailbox_state_filter' и для типов 'asterisk-publication' с использованием 'device_state_filter' и 'mailbox_state_filter'. Поскольку каждое событие отправлено или получено, устройство или почтовый ящик передается регулярному выражению, и если оно не совпадает - событие останавливается.

Пример

```
[instance1]
type=endpoint

[instance1-devicestate]
type=outbound-publish
server_uri=sip:instance2@172.16.10.1
event=asterisk-devicestate

[instance1-mwi]
type=outbound-publish
server_uri=sip:instance2@172.16.10.1
event=asterisk-mwi

[instance1]
type=inbound-publication
event_asterisk-devicestate=instance1
event_asterisk-mwi=instance1

[instance1]
type=asterisk-publication
devicestate_publish=instance1-devicestate
mailboxstate_publish=instance1-mwi
device_state=yes
device_state_filter=^PJSIP/
mailbox_state=yes
mailbox_state_filter=^1000
```

Это основывается на начальной конфигурации для экземпляра № 2, но добавляет фильтрацию полученных событий. Принимаются только события о состоянии устройства, относящиеся к конечным точкам PJSIP. Также будут приниматься только события состояний почтовых ящиков для почтовых ящиков, начинающихся с 1000.

---

Эта конфигурация неидеальна, так как экземпляр публикации (instance1) будет по-прежнему отправлять изменения состояний устройств и почтовых ящиков для instance1, что приводит к потере пропускной способности.

---

###### Свежий запуск

Когда модуль res_pjsip_publish_asterisk загружен - он отправляет свои текущие состояния для всех применимых устройств и почтовых ящиков всем настроенным типам публикации. Экземпляры могут быть дополнительно сконфигурированы для отправки запроса на обновление для типов публикации, а также путем установки опции 'devicestate_publish' и/или 'mailboxstate_publish' в типе 'asterisk-publication'. Этот запрос на обновление заставляет удаленные экземпляры отправлять текущие состояния для всех применимых устройств и почтовых ящиков обратно, что приводит к тому, что потенциально недавно запущенный Asterisk обновляется со своими пирами.

##### Configuring chan_sip for Presence Subscriptions

###### Overview
This page is a rough guide to get you configuring chan_sip and Asterisk to accept subscriptions for presence (in this case, Extension State) and notify the subscribers of state changes.

###### Requirements

You should understand the basics of
* Device State and Extension State and Hints
* Configuring SIP peers in sip.conf

###### General Process

**Overview**

It is best to consider this configuration in the context of a very simplified use case. It should illustrate the overall concept, as well as the ability for Extension State to aggregate Device States.

The case is that our administrator wants the user device of SIP/Alice to display the presence of Bob. Bob has two devices, SIP/Bob-mobile and SIP/Bob-desk. He could be on either device at any one time, so we want to map them both to the same Hint. That way, when Alice subscribes to the Hint, she'll get the aggregated Extension State of Bob's devices. That means if either of Bobs phones are busy, then the extension state will be busy. Then Alice knows that Bob is busy without having to have a separate light for each of Bob's phones.

Figure 1 should illustrate the overall relationships of the different elements involved.

Then following down the page you can find detail on configuring the three major elements, SIP configuration options, hints in dialplan, and configuring a phone to subscribe.

###### Configure SIP options
Since this is not a guide on configuring SIP peers, we'll show a very simple sip.conf  with only enough configuration to point out where you might set
specific chan_sip State and Presence Options.

```
[general]
callcounter=yes
[Alice]
type=friend
subscribecontext=default
allowsubscribe=yes
[Bob-mobile]
type=friend
busylevel=1
[Bob-desk]
type=friend
busylevel=1
```

We are setting one option in the general section, and then a few options across the three SIP peers involved.

callcounter and busylevel are the most essential options. callcounter needs to be enabled for chan_sip to provide accurate device. busylevel=1 says we want the device states of those peers to show busy if they have at least one call in progress. The subscribecontext option tells Asterisk which dialplan context to look for the hint. allowsubscribe says that we will allow subscriptions for that peer. It is really set to yes by default, but we are defining it here to demonstrate that you could allow and disallow subscriptions on a per-peer basis if you wanted.

![](/pics/chan_sip_pic1.png)

This diagram is purposefully simplified to only show the relationships between the elements involved in this configuration.

###### Configure Hints

Hints are configured in Asterisk dialplan (extensions.conf). This is where you map Device State identifiers or Presence State identifiers to a hint, which will then be subscribed to by one or more SIP User Agents.

For our example we need to define a hint mapping 6001 to Bob's two devices.

```
[default]
exten = 6001,hint,SIP/Bob-mobile&SIP/Bob-desk
```

Defining the hint is pretty straightforward and follows the syntax discussed in the Extension State and Hints section.

Notice that we put it in the context we set in subscribecontext in sip.conf earlier. Otherwise we would need to make sure it is in the same context that the SIP peer uses (defined with "context").

If you have restarted Asterisk to load the hints, then you can check to make sure they are configured with "core show hints"

```
*CLI> core show hints
-= Registered Asterisk Dial Plan Hints =-
6001@default : SIP/Bob-mobile&SIP/B State:Unavailable Watchers 0
```

You'll see the state changes to Idle or something else if you have your sip.conf configured properly and the two SIP devices are at least available.

###### Configure Subscriber

You should configure your SIP User Agent (soft-phone, hard-phone, another phone application like Asterisk) to subscribe to the hint. In this case that is SIP/Alice and we want her phone to subscribe to 6001.

The process will be different for every phone, and keep in mind that some phones may not support Asterisk's state notification. With most phones it'll be a matter of adding a "contact" to a contact list, buddy list, or address book and then making sure that SIP presence is enabled in the options.

If you want to submit a guide for a specific phone, feel free to comment on this page or submit it to the Asterisk issue tracker.

###### Operation

Typically as soon as you add the contact or subscription on the phone then it will attempt to SUBSCRIBE to Asterisk.

If you haven't done so, restart Asterisk and then restart the SIP User Agent client doing the subscribing.

The flow of SIP messaging can differ based on configuration, but typically looks like this for a peer that requires authentication:

```
SIP/Alice                     Asterisk
----------------------------------------
SUBSCRIBE          --->
                   <---       401 Unauthorized
SUBSCRIBE(w/ Auth) --->
                   <---       200 OK
                   <---       NOTIFY
200 OK             --->
```

In the expanding frame below is a SIP trace of a successful subscription for reference. You could see this on your own system by running "sip set debug on" and then watching for the subscription. You might have to restart your phone again or re-add a contact to see it.

Click to see the subscription trace...

```
<--- SIP read from UDP:10.24.17.254:37509 --->
SUBSCRIBE sip:6001@10.24.18.124;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 10.24.17.254:37509;branch=z9hG4bK-d8754z-e5ecfde1f337b690-1---d8754zMax-Forwards: 70
Contact: <sip:Alice@10.24.17.254:37509;transport=UDP>
To: <sip:6001@10.24.18.124;transport=UDP>
From: <sip:Alice@10.24.18.124;transport=UDP>;tag=f51e9632
Call-ID: ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.
CSeq: 1 SUBSCRIBE
Expires: 1800
Accept: application/pidf+xml
Allow: INVITE, ACK, CANCEL, BYE, NOTIFY, REFER, MESSAGE, OPTIONS, INFO, SUBSCRIBE
Supported: replaces, norefersub, extended-refer, timer, X-cisco-serviceuri
User-Agent: Z 3.2.21357 r21103
Event: presence
Allow-Events: presence, kpml
Content-Length: 0
<------------->
--- (16 headers 0 lines) ---
Sending to 10.24.17.254:37509 (no NAT)
Creating new subscription
Sending to 10.24.17.254:37509 (no NAT)
list_route: route/path hop: <sip:Alice@10.24.17.254:37509;transport=UDP>
Found peer 'Alice' for 'Alice' from 10.24.17.254:37509
<--- Transmitting (no NAT) to 10.24.17.254:37509 --->
SIP/2.0 401 Unauthorized
Via: SIP/2.0/UDP 10.24.17.254:37509;branch=z9hG4bK-d8754z-e5ecfde1f337b690-1---d8754z-;received=10.24.17.254
From: <sip:Alice@10.24.18.124;transport=UDP>;tag=f51e9632
To: <sip:6001@10.24.18.124;transport=UDP>;tag=as46a6e039
Call-ID: ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.
CSeq: 1 SUBSCRIBE
Server: Asterisk PBX SVN-branch-12-r413487
Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, SUBSCRIBE, NOTIFY, INFO, PUBLISH, MESSAGE
Supported: replaces, timer
WWW-Authenticate: Digest algorithm=MD5, realm="asterisk", nonce="522456f4"
Content-Length: 0
<------------>
Scheduling destruction of SIP dialog 'ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.' in 32000 ms (Method: SUBSCRIBE)
<--- SIP read from UDP:10.24.17.254:37509 --->
SUBSCRIBE sip:6001@10.24.18.124;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 10.24.17.254:37509;branch=z9hG4bK-d8754z-c6908de6f0126edf-1---d8754zMax-Forwards: 70
Contact: <sip:Alice@10.24.17.254:37509;transport=UDP>
To: <sip:6001@10.24.18.124;transport=UDP>
From: <sip:Alice@10.24.18.124;transport=UDP>;tag=f51e9632
Call-ID: ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.
CSeq: 2 SUBSCRIBE
Expires: 1800

Accept: application/pidf+xml
Allow: INVITE, ACK, CANCEL, BYE, NOTIFY, REFER, MESSAGE, OPTIONS, INFO, SUBSCRIBE
Supported: replaces, norefersub, extended-refer, timer, X-cisco-serviceuri
User-Agent: Z 3.2.21357 r21103
Authorization: Digest
username="Alice",realm="asterisk",nonce="522456f4",uri="sip:6001@10.24.18.124;transport=UDP",response="6d66dcad8c176aa3ef7bae
c7680d2445",algorithm=MD5
Event: presence
Allow-Events: presence, kpml
Content-Length: 0
<------------->
--- (17 headers 0 lines) ---
Creating new subscription
Sending to 10.24.17.254:37509 (no NAT)
Found peer 'Alice' for 'Alice' from 10.24.17.254:37509
Looking for 6001 in default (domain 10.24.18.124)
Scheduling destruction of SIP dialog 'ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.' in 1810000 ms (Method: SUBSCRIBE)
<--- Transmitting (no NAT) to 10.24.17.254:37509 --->
SIP/2.0 200 OK
Via: SIP/2.0/UDP 10.24.17.254:37509;branch=z9hG4bK-d8754z-c6908de6f0126edf-1---d8754z-;received=10.24.17.254
From: <sip:Alice@10.24.18.124;transport=UDP>;tag=f51e9632
To: <sip:6001@10.24.18.124;transport=UDP>;tag=as46a6e039
Call-ID: ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.
CSeq: 2 SUBSCRIBE
Server: Asterisk PBX SVN-branch-12-r413487
Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, SUBSCRIBE, NOTIFY, INFO, PUBLISH, MESSAGE
Supported: replaces, timer
Expires: 1800
Contact: <sip:6001@10.24.18.124:5060>;expires=1800
Content-Length: 0
<------------>
set_destination: Parsing <sip:Alice@10.24.17.254:37509;transport=UDP> for address/port to send to
set_destination: set destination to 10.24.17.254:37509
Reliably Transmitting (no NAT) to 10.24.17.254:37509:
NOTIFY sip:Alice@10.24.17.254:37509;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 10.24.18.124:5060;branch=z9hG4bK14aacddc
Max-Forwards: 70
From: <sip:6001@10.24.18.124;transport=UDP>;tag=as46a6e039
To: <sip:Alice@10.24.18.124;transport=UDP>;tag=f51e9632
Contact: <sip:6001@10.24.18.124:5060>
Call-ID: ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.
CSeq: 102 NOTIFY
User-Agent: Asterisk PBX SVN-branch-12-r413487
Subscription-State: active
Event: presence
Content-Type: application/pidf+xml
Content-Length: 530
<?xml version="1.0" encoding="ISO-8859-1"?>
<presence xmlns="urn:ietf:params:xml:ns:pidf"
xmlns:pp="urn:ietf:params:xml:ns:pidf:person"
xmlns:es="urn:ietf:params:xml:ns:pidf:rpid:status:rpid-status"
xmlns:ep="urn:ietf:params:xml:ns:pidf:rpid:rpid-person"
entity="sip:Alice@10.24.18.124">
<pp:person><status>
<ep:activities><ep:away/></ep:activities>
</status></pp:person>
<note>Unavailable</note>
<tuple id="6001">
<contact priority="1">sip:6001@10.24.18.124</contact>
<status><basic>closed</basic></status>
</tuple>
</presence>
---
<--- SIP read from UDP:10.24.17.254:37509 --->
SIP/2.0 200 OK
Via: SIP/2.0/UDP 10.24.18.124:5060;branch=z9hG4bK14aacddc
Contact: <sip:Alice@10.24.17.254:37509;transport=UDP>
To: <sip:Alice@10.24.18.124;transport=UDP>;tag=f51e9632
From: <sip:6001@10.24.18.124;transport=UDP>;tag=as46a6e039
Call-ID: ZjE2ZDAwYThiOTA2MzYxOWEwNTEwMjc1ZGIxNTk3NDU.
CSeq: 102 NOTIFY
User-Agent: Z 3.2.21357 r21103
Content-Length: 0
<------------->
--- (9 headers 0 lines) ---
```

Once the subscription has taken place, there is a command to list them. "sip show subscriptions"

```
*CLI> sip show subscriptions
Peer User Call ID Extension Last state Type Mailbox Expiry
10.24.17.254 Alice ZjE2ZDAwYThiOTA 6001@default Unavailable pidf+xml <none> 001800
1 active SIP subscription
```

From this point onward, Asterisk should send out a SIP NOTIFY to the Alice peer whenever state changes for any of the devices mapped to the hint 6001.
Alice's phone should then reflect that state on its display.

#### Настройка res_pjsip

##### Настройка res_pjsip для подписок на присутствие

Раздел в разработке - эта страница не завершена!

###### Возможности

Драйвер канала pjsip Asterisk предоставляет те же возможности подписки на присутствие что и `chan_sip`. Это означает, что присутствие [RFC 3856](http://tools.ietf.org/html/rfc3856) и [RFC4235](http://www.rfc-editor.org/rfc/rfc4235.txt) поддерживает диалоговые данные. Подписки на присутствие поддерживают тела [RFC 3863](https://tools.ietf.org/html/rfc3863) PIDF+XML, а также [XPIDF+XML](https://tools.ietf.org/html/draft-rosenberg-impp-pidf-00). Кроме того, Asterisk также поддерживает подписку на списки ресурсов присутствия [RFC 4662](https://tools.ietf.org/html/rfc4662).

###### Конфигурация

Если вы знакомы с настройкой подписок в `chan_sip`, то это должно быть вам знакомо. Настройка присутствия выполняется с использованием приоритета "hint" для расширения в `extensions.conf`.

```
; extensions.conf
[default]
exten => 1000,hint,PJSIP/alice
```

Строка, показанная здесь, похожа на любую нормальную строку в диалплане, за исключением того, что вместо номера приоритета или метки указано слово "hint". hint используется для связи состояния отдельных устройств с состоянием расширения диалплана. Английский перевод строки диалплана будет звучать так: "используйте состояние устройства PJSIP/alice в качестве основы для состояния расширения 1000". Когда конечные точки PJSIP подписываются на присутствие, они подписываются на состояние расширения в диалплане. Предоставляя hint (подсказку) в диалплане вы создаете необходимую ассоциацию, чтобы узнать, какое устройство (или устройства) являются релевантными. Для примера, приведенного выше, это означает, что если кто-то подписывается на состояние расширения 1000, то ему будет сообщено состояние PJSIP/alice. Дополнительные сведения о состоянии устройства см. на [этой странице](fundamentals.md#device-state).

Существует два варианта конечных точек, влияющих на наличие подписок в `pjsip.conf`. Параметр `allow_subscribe` определяет, разрешено ли Asterisk получать запросы на подписку от конечной точки. По умолчанию функция `allow_subscribe` включена. Другим параметром, влияющим на подписку на присутствие, является параметр `context`. Этот параметр используется для определения контекста диалплана, в котором следует искать подписываемое расширение. Учитывая приведенный выше фрагмент диалплана, если конечная точка, которая подписывается на расширение 1000, должна подписаться на подсказку 1000@default, то контекст подписывающейся конечной точки должен быть установлен в "default". Обратите внимание, что если параметр `context` имеет значение, отличное от "default", то Asterisk будет искать подсказку в том контексте.

Для правильной работы подписок на присутствие необходимо загрузить некоторые модули. Вот список необходимых модулей:
* `res_pjsip.so`: Ядро кода PJSIP в Asterisk.
* `res_pjsip_pubsub.so`: код, реализующий логику SUBSCRIBE/NOTIFY, на основе которой строятся отдельные обработчики событий.
* `res_pjsip_exten_state.so`: обрабатывает события "presence" и "dialog".
* `res_pjsip_pidf_body_generator.so`: этот модуль генерирует тела сообщений application/pidf+xml. Требуется для большинства подписок на событие "presence".
* `res_pjsip_xpidf_body_generator.so`: этот модуль генерирует тела сообщений application/xpidf+xml. Требуется для некоторых подписок на событие "presence".
* `res_pjsip_dialog_info_body_generator.so`: требуется для подписки на событие "dialog". Этот модуль генерирует тела сообщений application/dialog-info.

Если вы не уверены какое событие или какой тип тела используется вашим устройством для подписки на присутствие, обратитесь к руководству производителя устройства для получения дополнительной информации.

###### Кастомизация присутствия

**Digium Presence**

Телефоны Digium оснащены пользовательским дополнением к базовому формату присутствия PIDF+XML, которое позволяет понимать присутствие XMPP-типа. Чтобы добавить его, hint необходимо изменить, включив в него дополнительное состояние присутствия, например:

```
; extensions.conf
[default]
exten => 1000,hint,PJSIP/alice,CustomPresence:alice
```

Это означает, что обновления состояния присутствия CustomPresence:alice также будут передаваться подписчикам на расширение 1000. Дополнительные сведения о состоянии присутствия в Asterisk см. в разделе на [этой странице](presence-state).

Модуль `res_pjsip_pidf_digium_body_supplement.so` должен быть загружен, чтобы сообщать дополнительные сведения о присутствии.

**Расширенный Presence (ограничено)**

Некоторые расширенные дополнения присутствия, которые были в `chan_sip`, также были перенесены в драйвер канала PJSIP. Это крайне ограниченная реализация "деятельностного" элемента личности. Модуль `res_pjsip_pidf_eyebeam_body_supplement.so` необходим для добавления этой функциональности.

### Inter-Asterisk eXchange protocol, version 2 (IAX2)
### DAHDI
### Local Channel
### Motif
### mISDN
### Mobile Channel
### Unistim
### Skinny
### RTP Packetization

## Dialplan
## Features
## Applications
## Functions
## Reporting
## Interfaces

##### Публикация состояний расширений

###### Фон

В PJSIP, начиная с Asterisk14, существует функциональность, позволяющая публиковать состояние расширения в другой сущности, обычно называемой сборщиком событий состояния. Вместо того чтобы каждое устройство подписывалось на Asterisk и получало уведомление об изменении состояния расширения - PJSIP можно настроить для отправки одного запроса на публикацию для каждого изменения состояния расширения другому объекту. Эти запросы на публикацию запускаются на основе изменений состояний расширения, внесенных в hint'ы в диалплане.

![](pics/publishing.png)

###### Зачем это делать

Публикация состояний расширения позволяет другому объекту обрабатывать функции подписки и уведомления. Каждое устройство подписывается на сборщика событий состояний и получает от него сообщения NOTIFY. Это может масштабироваться еще больше, поскольку в Asterisk присутствует меньшее состояние, а также позволяет использовать несколько экземпляров Asterisk, при этом делая состояние расширения доступным для всех из центрального сборщика событий состояния.

![](pics/publishing_full.png)

###### Что можно публиковать?

PJSIP имеет подключаемую систему тел. Любой тип, на который можно подписаться для состояния расширения - может быть опубликован. На момент написания этой статьи доступны следующие типы тел:

* application/dialog-info+xml
* application/pidf+xml
* application/xpidf+xml
* application/cpim-pidf+xml

Запрос PUBLISH будет содержать то же тело, что и запрос на уведомление.

###### Конфигурация

Публикация состояния расширения настраивается путем указания **исходящей публикации** в файле pjsip.conf. Это говорит PJSIP как опубликовать другой объект, и дает ему информацию о том, что нужно опубликовать. Однако исходящая публикация состояния расширения имеет некоторые дополнительные аргументы, которые позволяют осуществлять больший контроль.

Параметр **@body** указывает, какой тип тела следует опубликовать. Это обязательный вариант.

Параметр **@context** задает фильтр для контекста. Это регулярное выражение и является необязательным.

Параметр **@exten** задает фильтр для расширений. Это регулярное выражение и является необязательным.

Дополнительным параметром, который требуется для исходящей публикации, является параметр **multi_user**. Он обеспечивает поддержку в модуле исходящей публикации для публикации различным пользователям. Это необходимо для публикации состояния расширения, чтобы можно было опубликовать конкретное расширение. Без включения этой опции все запросы на публикацию будут отправляться одному и тому же пользователю.

###### Пример понфигурации

Эта конфигурация ограничила бы исходящую публикацию только изменениями состояния расширения в результате хинта с именем "1000" в контексте "users".

```
[test-esc]
type=outbound-publish
server_uri=sip:172.16.0.100
from_uri=sip:172.16.0.100
event=dialog
multi_user=yes
@body=application/dialog-info+xml
@context=^users
@exten=^1000
```
Эта конфигурация будет ограничивать исходящую публикацию всеми изменениями состояния расширения в результате хинтов в контексте "users".

```
[test-esc]
type=outbound-publish
server_uri=sip:172.16.0.100
from_uri=sip:172.16.0.100
event=dialog
multi_user=yes
@body=application/dialog-info+xml
@context=^users
```

Вы также не ограничены одной настроенной исходящей публикацией. Вы можете иметь их столько, сколько захотите, при условии что они имеют разные имена. Каждая из них может перейти на один и тот же сервер с разным типом тела или на разные серверы.

###### А как насчет того, чтобы сделать это более динамичным?

В рамках работы по реализации публикации состояния расширения была также создана концепция **autohints**. Автоответчики создаются автоматически в результате изменения состояния устройства. Используемое имя расширения - это имя устройства без указания технологии. Они могут быть включены с помощью установки "autohints=yes" в контексте в extensions.conf вот так:

```
[users]
autohints=yes
```

Например, если после включения происходит изменение состояния устройства для "PJSIP/alice" и не существует хинта с именем "alice", то она будет автоматически создана вместо явного определения следующего:

```
exten => alice,hint,PJSIP/alice
```

Несмотря на добавление после запуска, эта подсказка все равно будет предоставлена публикации состояния расширения для публикации.

###### Другая организация

На протяжении всей этой страницы я упоминал еще одну сущность; но что вы можете использовать? Kamailio! В Kamailio есть поддержка сборщика событий состояний, доступная с помощью [модуля присутствия](http://kamailio.org/docs/modules/4.4.x/modules/presence.html). Он может быть настроен для приема запросов на подписку и публикацию, сохранения информации в базе данных и последующей отправки сообщений NOTIFY на каждое подписанное устройство. Модуль экспортирует функции handle_publish и handle_subscribe для обработки каждой из них.

Этот модуль прекрасно работает с поддержкой публикации состояния расширения PJSIP. Конфигурация Asterisk должна использовать URI для сервера Kamailio, а сервер Kamailio должен явно доверять трафику от экземпляра Asterisk, либо необходимо настроить аутентификацию.
