# Available Pages:

[About the Project](about_the_project.md)
A Brief History of the Asterisk Project

Asterisk as a Swiss Army Knife of Telephony

Asterisk Versions

License Information

Voice Prompts and Music on Hold License

[Getting Started](getting_started.md)

Beginning Asterisk

Installing Asterisk

Installing AsteriskNOW

Upgrading AsteriskNOW

Upgrading AsteriskNOW Version 3.0.1 to 5.211.65

Upgrading AsteriskNOW Version 5.211.65
            Installing Asterisk From Source
                What to Download?
                Untarring the Source
                Building and Installing DAHDI
                Building and Installing LibPRI
                Building and Installing pjproject
                Checking Asterisk Requirements
                Using Menuselect to Select Asterisk Options
                Building and Installing Asterisk
                Installing Sample Files
                Installing Initialization Scripts
                Validating Your Installation
            Alternate Install Methods
                Asterisk Packages
                    Historical Packaging Information
            Installing Asterisk on Non-Linux Operating Systems
                Asterisk on (Open)Solaris
        Hello World
    Operation
        System Requirements
            Compiler
            System Libraries
        Running Asterisk
            Stopping and Restarting Asterisk From The CLI
        Maintenance and Upgrades
            Asterisk Backups
            Updating or Upgrading Asterisk
        Logging
            Basic Logging Commands
            Basic Logging Start-up Options
            Call Identifier Logging
            Collecting Debug Information
            Queue Logs
            Verbosity in Core and Remote Consoles
        Asterisk Command Line Interface
            Connecting to the Asterisk CLI
            CLI Syntax and Help Commands
            Creating and Manipulating Channels from the CLI
            Simple CLI Tricks
        Asterisk Audio and Video Capabilities
    Fundamentals
        Asterisk Architecture
            Asterisk Architecture, The Big Picture
            Types of Asterisk Modules
                Channel Driver Modules
                Dialplan Application Modules
                Dialplan Function Modules
                Resource Modules
                Codec Modules
                File Format Drivers
                Call Detail Record (CDR) Drivers
                Call Event Log (CEL) Driver Modules
                Bridging Modules
        Directory and File Structure
        Asterisk Configuration
            Asterisk Configuration Files
                Config File Format
                    Sections and Settings
                    Objects
                Comments
                    Comments on a Single Line
                    Block Comments
                Using The include, tryinclude and exec Constructs
                Adding to an existing section
                Templates
                    Template Syntax
                    Using Templates
            Database Support Configuration
                Realtime Database Configuration
                SIP Realtime, MySQL table structure
            Sorcery
                Sorcery Caching
        Asterisk Internal Database
            SQLite3 astdb back-end
        Key Concepts
            Bridges
            Channels
            Frames
                Audiohooks
            States and Presence
                Device State
                Extension State and Hints
                Presence State
                Querying and Manipulating State
            The Stasis Message Bus
    Configuration
        Core Configuration
            Asterisk Main Configuration File
            Timing Interfaces
            Asterisk Builtin mini-HTTP Server
            Logging Configuration
            Asterisk CLI Configuration
            Configuring the Asterisk Module Loader
            Configuring Localized Tone Indications
            Video Telephony
            Video Console
            Named ACLs
        Channel Drivers
            SIP
                Configuring chan_sip
                    chan_sip State and Presence Options
                    Configuring chan_sip for IPv6
                    Configuring chan_sip for Presence Subscriptions
                Configuring res_pjsip
                    PJSIP Configuration Sections and Relationships
                    res_pjsip Configuration Examples
                    Migrating from chan_sip to res_pjsip
                    Dialing PJSIP Channels
                    Configuring res_pjsip to work through NAT
                    Setting up PJSIP Realtime
                    Exchanging Device and Mailbox State Using PJSIP
                    Configuring res_pjsip for Presence Subscriptions
                    Resource List Subscriptions (RLS)
                    Configuring Outbound Registrations
                    Asterisk PJSIP Troubleshooting Guide
                    res_pjsip Remote Attended Transfers
                    PJSIP Transport Selection
                    PJSIP Configuration Wizard
                    Configuring res_pjsip for IPv6
                    Publishing Extension State
                Real-time Text (T.140)
            Inter-Asterisk eXchange protocol, version 2 (IAX2)
                Why IAX2?
                Introduction to IAX2
                IAX2 Configuration
                    Configuring chan_iax2 for IPv6
                IAX2 Jitterbuffer
                IAX2 Security
            DAHDI
            Local Channel
                Local Channel Examples
                    Delay Dialing Devices Example
                    Dialing Destinations with Different Information
                    Trivial Local Channel Example
                    Using Callfiles and Local Channels
                Local Channel Optimization
                Local Channel Modifiers
            Motif
                Calling using Google
            mISDN
                Introduction to mISDN
                mISDN Features
                mISDN Fast Installation Guide
                mISDN Pre-Requisites
                mISDN Configuration
                mISDN CLI Commands
                mISDN Variables
                mISDN Debugging and Bug Reports
                mISDN Examples
                mISDN Known Problems
            Mobile Channel
                Introduction to the Mobile Channel
                Mobile Channel Features
                Mobile Channel Requirements
                Mobile Channel Concepts
                Configuring chan_mobile
                Using chan_mobile
                Mobile Channel Dialplan Hints
                MobileStatus Application
                Mobile Channel DTMF Debouncing
                Mobile Channel SMS Sending and Receiving
                Mobile Channel Debugging
            Unistim
                Introduction to the Unistim channel
                Protocol information
            Skinny
                Skinny call logging
                Skinny Dev Notes
                    Keepalives
                    Skinny device stuff
            RTP Packetization
        Dialplan
            Contexts, Extensions, and Priorities
            Special Dialplan Extensions
            Include Statements
                Include Statements Basics
                Using Include Statements to Create Classes of Service
            Switch Statements
            Variables
                Channel Variables
                    Parameter Quoting
                    Setting and Substituting Channel Variables
                    Variable Inheritance
                    Selecting Characters from Variables
                    Asterisk Standard Channel Variables
                        Application return values
                        Various application variables
                        MeetMe Channel Variables
                        VoiceMail Channel Variables
                        VMAuthenticate Channel Variables
                        DUNDiLookup Channel Variables
                        chan_dahdi Channel Variables
                        chan_sip Channel Variables
                        chan_agent Channel Variables
                        Dial Channel Variables
                        Chanisavail() Channel Variables
                        Dialplan Macros Channel Variables
                        ChanSpy Channel Variables
                        Open Settlement Protocol (OSP) Channel Variables
                        Digit Manipulation Channel Variables
                    Case Sensitivity
                Global Variables Basics
                Manipulating Variables Basics
                Using the CONTEXT, EXTEN, PRIORITY, UNIQUEID, and CHANNEL Variables
            Pattern Matching
            Subroutines
                GoSub
                Hangup Handlers
                Macros
                Party ID Interception Macros and Routines
                Pre-Bridge Handlers
                Pre-Dial Handlers
            Expressions
                Spaces Inside Variables Values
                Operators
                Floating Point Numbers
                Expr2 Built-in Functions
                Expressions Examples
                Numbers Vs. Strings
                Expression Parsing Errors
                NULL Strings
                Warnings about Expressions
                Expression Parser Incompatibilities
                Expression Debugging Hints
            Conditional Applications
        Features
            Feature Code Call Transfers
            One-Touch Features
            Call Pickup
            Built-in Dynamic Features
            Custom Dynamic Features
            Call Parking
        Applications
            Answer, Playback, and Hangup Applications
            Bridge Application
            Dial Application
            Directory Application
            Early Media and the Progress Application
            External IVR Interface
            MacroExclusive
            The Read Application
            The Verbose and NoOp Applications
            SMS
            Voicemail
                ODBC Voicemail Storage
                IMAP Voicemail Storage
                    IMAP VM Storage Installation Notes
                    IMAP VM Storage Voicemail.conf Modifications
                    Voicemail and IMAP Folders
                    Separate vs. Shared E-mail Accounts
                    IMAP Server Implementations
                    IMAP Voicemail Quota Support
                    IMAP Voicemail Application Notes
                Message Waiting Indication
            Conferencing Applications
                ConfBridge
                    ConfBridge AMI Actions
                    ConfBridge AMI Events
                    ConfBridge CLI Commands
                    ConfBridge Configuration
                    ConfBridge Functions
                    ConfBridge Sound Prompts
        Functions
            Simple Message Desk Interface (SMDI) Integration
        Reporting
            Call Detail Records (CDR)
                CDR Variables
                CDR Storage Backends
                    MSSQL CDR Backend
                    MySQL CDR Backend
                    PostgreSQL CDR Backend
                    SQLite 2 CDR Backend
                    SQLite 3 CDR Backend
                    RADIUS CDR Backend
            Channel Event Logging (CEL)
                CEL Design Goals
                CEL Applications and Functions
                CEL Configuration Files
                CEL Configuration Examples
                    MSSQL CEL Backend
                    PostgreSQL CEL Backend
                    RADIUS CEL Backend
        Interfaces
            Asterisk Calendaring
                Configuring Asterisk Calendaring
                Calendaring Dialplan Functions
                Calendaring Dialplan Examples
            Asterisk Call Files
            Asterisk Gateway Interface (AGI)
            Asterisk Manager Interface (AMI)
                The Asterisk Manager TCP IP API
                AMI Command Syntax
                AMI Manager Commands
                AMI Examples
                Ensuring all modules are loaded with AMI
                Some Standard AMI Headers
                Asynchronous Javascript Asterisk Manager (AJAM)
                    Setting up the Asterisk HTTP server
                    Allow Manager Access via HTTP
                    Integration with other web servers
                Asterisk Manager Interface (AMI) Changes
                    AMI 1.1 Changes
                AMI Libraries and Frameworks
            Asterisk REST Interface (ARI)
                Getting Started with ARI
                    Using Swagger to Drive ARI
                Asterisk Configuration for ARI
                Introduction to ARI and Channels
                    ARI and Channels: Manipulating Channel State
                    ARI and Channels: Simple Media Manipulation
                    ARI and Channels: Handling DTMF
                Introduction to ARI and Bridges
                    ARI and Bridges: Holding Bridges
                    ARI and Bridges: Basic Mixing Bridges
                    ARI and Bridges: Bridge Operations
                Introduction to ARI and Media Manipulation
                    ARI and Media: Part 1 - Recording
                    ARI and Media: Part 2 - Playbacks
                The Asterisk Resource
                    ARI Push Configuration
            Back-end Database and Realtime Connectivity
                cURL
                ODBC
                    Configuring res_odbc
                    Getting Asterisk Connected to MySQL via ODBC
                SQLite Tables
                Storing Voicemail in PostgreSQL via ODBC
            Distributed Device State
                Corosync
                Distributed Device State with AIS
                Distributed Device State with XMPP PubSub
            Simple Network Management Protocol (SNMP) Support
                Asterisk MIB Definitions
                Digium MIB Definitions
            Speech Recognition API
            Utilizing the StatsD Dialplan Application
    Deployment
        Basic PBX Functionality
            The Most Basic PBX
            Creating SIP Accounts
            Registering Phones to Asterisk
            Creating Dialplan Extensions
            Making a Phone Call
            Auto-attendant and IVR Menus
                Background and WaitExten Applications
                Goto Application and Priority Labels
                SayDigits, SayNumber, SayAlpha, and SayPhonetic Applications
                Creating a Simple IVR Menu
                Handling Special Extensions
                Record Application
            Adding Voice Mail to Dialplan Extensions
                Configuring Voice Mail Boxes
        Deployment In Your Network
        Emergency Calling
        Important Security Considerations
            Network Security
            Dialplan Security
            Log Security
            Asterisk Security Webinars
        Privacy Configuration
            FTC Don't Call List
            Fighting Autodialers
            Fighting Empty Caller ID
            Using Welcome Menus for Privacy
            Making life difficult for telemarketers
            Using Call Screening
            Call Screening Options
            Screening Calls with Recorded Introductions
        Internationalization and Localization
            Asterisk Sounds Packages
                Getting the Sounds Tools
                About the Sounds Tools
            Sound Prompt Searching based on Channel Language
        Troubleshooting
            SIP Retransmissions
            Troubleshooting Asterisk Module Loading
            Unable to connect to remote Asterisk
        IPv6 Support
        PSTN Connectivity
            Advice of Charge
            Caller ID in India
            Signaling System Number 7
        Secure Calling
            Secure Calling Specifics
            Secure Calling Tutorial
                Installing Blink SIP client
            SIP TLS Transport
        Reference Use Cases for Asterisk
            Super Awesome Company
    Asterisk Security Vulnerabilities
    Asterisk Community
        Asterisk Community Code of Conduct
        Asterisk Community Services
        Asterisk Issue Guidelines
        Asterisk Module Support States
        Community Services Signup
        IRC
        Mailing Lists
        Wiki Organization and Style Guide
    New in 14
    Upgrading to Asterisk 14
    Asterisk 14 Command Reference
        Asterisk 14 AGI Commands
            Asterisk 14 AGICommand_answer
            Asterisk 14 AGICommand_asyncagi break
            Asterisk 14 AGICommand_channel status
            Asterisk 14 AGICommand_control stream file
            Asterisk 14 AGICommand_database del
            Asterisk 14 AGICommand_database deltree
            Asterisk 14 AGICommand_database get
            Asterisk 14 AGICommand_database put
            Asterisk 14 AGICommand_exec
            Asterisk 14 AGICommand_get data
            Asterisk 14 AGICommand_get full variable
            Asterisk 14 AGICommand_get option
            Asterisk 14 AGICommand_get variable
            Asterisk 14 AGICommand_gosub
            Asterisk 14 AGICommand_hangup
            Asterisk 14 AGICommand_noop
            Asterisk 14 AGICommand_receive char
            Asterisk 14 AGICommand_receive text
            Asterisk 14 AGICommand_record file
            Asterisk 14 AGICommand_say alpha
            Asterisk 14 AGICommand_say date
            Asterisk 14 AGICommand_say datetime
            Asterisk 14 AGICommand_say digits
            Asterisk 14 AGICommand_say number
            Asterisk 14 AGICommand_say phonetic
            Asterisk 14 AGICommand_say time
            Asterisk 14 AGICommand_send image
            Asterisk 14 AGICommand_send text
            Asterisk 14 AGICommand_set autohangup
            Asterisk 14 AGICommand_set callerid
            Asterisk 14 AGICommand_set context
            Asterisk 14 AGICommand_set extension
            Asterisk 14 AGICommand_set music
            Asterisk 14 AGICommand_set priority
            Asterisk 14 AGICommand_set variable
            Asterisk 14 AGICommand_speech activate grammar
            Asterisk 14 AGICommand_speech create
            Asterisk 14 AGICommand_speech deactivate grammar
            Asterisk 14 AGICommand_speech destroy
            Asterisk 14 AGICommand_speech load grammar
            Asterisk 14 AGICommand_speech recognize
            Asterisk 14 AGICommand_speech set
            Asterisk 14 AGICommand_speech unload grammar
            Asterisk 14 AGICommand_stream file
            Asterisk 14 AGICommand_tdd mode
            Asterisk 14 AGICommand_verbose
            Asterisk 14 AGICommand_wait for digit
        Asterisk 14 AMI Actions
            Asterisk 14 ManagerAction_AbsoluteTimeout
            Asterisk 14 ManagerAction_AgentLogoff
            Asterisk 14 ManagerAction_Agents
            Asterisk 14 ManagerAction_AGI
            Asterisk 14 ManagerAction_AOCMessage
            Asterisk 14 ManagerAction_Atxfer
            Asterisk 14 ManagerAction_BlindTransfer
            Asterisk 14 ManagerAction_Bridge
            Asterisk 14 ManagerAction_BridgeDestroy
            Asterisk 14 ManagerAction_BridgeInfo
            Asterisk 14 ManagerAction_BridgeKick
            Asterisk 14 ManagerAction_BridgeList
            Asterisk 14 ManagerAction_BridgeTechnologyList
            Asterisk 14 ManagerAction_BridgeTechnologySuspend
            Asterisk 14 ManagerAction_BridgeTechnologyUnsuspend
            Asterisk 14 ManagerAction_Challenge
            Asterisk 14 ManagerAction_ChangeMonitor
            Asterisk 14 ManagerAction_Command
            Asterisk 14 ManagerAction_ConfbridgeKick
            Asterisk 14 ManagerAction_ConfbridgeList
            Asterisk 14 ManagerAction_ConfbridgeListRooms
            Asterisk 14 ManagerAction_ConfbridgeLock
            Asterisk 14 ManagerAction_ConfbridgeMute
            Asterisk 14 ManagerAction_ConfbridgeSetSingleVideoSrc
            Asterisk 14 ManagerAction_ConfbridgeStartRecord
            Asterisk 14 ManagerAction_ConfbridgeStopRecord
            Asterisk 14 ManagerAction_ConfbridgeUnlock
            Asterisk 14 ManagerAction_ConfbridgeUnmute
            Asterisk 14 ManagerAction_ControlPlayback
            Asterisk 14 ManagerAction_CoreSettings
            Asterisk 14 ManagerAction_CoreShowChannels
            Asterisk 14 ManagerAction_CoreStatus
            Asterisk 14 ManagerAction_CreateConfig
            Asterisk 14 ManagerAction_DAHDIDialOffhook
            Asterisk 14 ManagerAction_DAHDIDNDoff
            Asterisk 14 ManagerAction_DAHDIDNDon
            Asterisk 14 ManagerAction_DAHDIHangup
            Asterisk 14 ManagerAction_DAHDIRestart
            Asterisk 14 ManagerAction_DAHDIShowChannels
            Asterisk 14 ManagerAction_DAHDITransfer
            Asterisk 14 ManagerAction_DataGet
            Asterisk 14 ManagerAction_DBDel
            Asterisk 14 ManagerAction_DBDelTree
            Asterisk 14 ManagerAction_DBGet
            Asterisk 14 ManagerAction_DBPut
            Asterisk 14 ManagerAction_DeviceStateList
            Asterisk 14 ManagerAction_DialplanExtensionAdd
            Asterisk 14 ManagerAction_DialplanExtensionRemove
            Asterisk 14 ManagerAction_Events
            Asterisk 14 ManagerAction_ExtensionState
            Asterisk 14 ManagerAction_ExtensionStateList
            Asterisk 14 ManagerAction_FAXSession
            Asterisk 14 ManagerAction_FAXSessions
            Asterisk 14 ManagerAction_FAXStats
            Asterisk 14 ManagerAction_Filter
            Asterisk 14 ManagerAction_FilterList
            Asterisk 14 ManagerAction_GetConfig
            Asterisk 14 ManagerAction_GetConfigJSON
            Asterisk 14 ManagerAction_Getvar
            Asterisk 14 ManagerAction_Hangup
            Asterisk 14 ManagerAction_IAXnetstats
            Asterisk 14 ManagerAction_IAXpeerlist
            Asterisk 14 ManagerAction_IAXpeers
            Asterisk 14 ManagerAction_IAXregistry
            Asterisk 14 ManagerAction_JabberSend_res_xmpp
            Asterisk 14 ManagerAction_ListCategories
            Asterisk 14 ManagerAction_ListCommands
            Asterisk 14 ManagerAction_LocalOptimizeAway
            Asterisk 14 ManagerAction_LoggerRotate
            Asterisk 14 ManagerAction_Login
            Asterisk 14 ManagerAction_Logoff
            Asterisk 14 ManagerAction_MailboxCount
            Asterisk 14 ManagerAction_MailboxStatus
            Asterisk 14 ManagerAction_MeetmeList
            Asterisk 14 ManagerAction_MeetmeListRooms
            Asterisk 14 ManagerAction_MeetmeMute
            Asterisk 14 ManagerAction_MeetmeUnmute
            Asterisk 14 ManagerAction_MessageSend
            Asterisk 14 ManagerAction_MixMonitor
            Asterisk 14 ManagerAction_MixMonitorMute
            Asterisk 14 ManagerAction_ModuleCheck
            Asterisk 14 ManagerAction_ModuleLoad
            Asterisk 14 ManagerAction_Monitor
            Asterisk 14 ManagerAction_MuteAudio
            Asterisk 14 ManagerAction_MWIDelete
            Asterisk 14 ManagerAction_MWIGet
            Asterisk 14 ManagerAction_MWIUpdate
            Asterisk 14 ManagerAction_Originate
            Asterisk 14 ManagerAction_Park
            Asterisk 14 ManagerAction_ParkedCalls
            Asterisk 14 ManagerAction_Parkinglots
            Asterisk 14 ManagerAction_PauseMonitor
            Asterisk 14 ManagerAction_Ping
            Asterisk 14 ManagerAction_PJSIPNotify
            Asterisk 14 ManagerAction_PJSIPQualify
            Asterisk 14 ManagerAction_PJSIPRegister
            Asterisk 14 ManagerAction_PJSIPShowEndpoint
            Asterisk 14 ManagerAction_PJSIPShowEndpoints
            Asterisk 14 ManagerAction_PJSIPShowRegistrationsInbound
            Asterisk 14 ManagerAction_PJSIPShowRegistrationsOutbound
            Asterisk 14 ManagerAction_PJSIPShowResourceLists
            Asterisk 14 ManagerAction_PJSIPShowSubscriptionsInbound
            Asterisk 14 ManagerAction_PJSIPShowSubscriptionsOutbound
            Asterisk 14 ManagerAction_PJSIPUnregister
            Asterisk 14 ManagerAction_PlayDTMF
            Asterisk 14 ManagerAction_PresenceState
            Asterisk 14 ManagerAction_PresenceStateList
            Asterisk 14 ManagerAction_PRIDebugFileSet
            Asterisk 14 ManagerAction_PRIDebugFileUnset
            Asterisk 14 ManagerAction_PRIDebugSet
            Asterisk 14 ManagerAction_PRIShowSpans
            Asterisk 14 ManagerAction_QueueAdd
            Asterisk 14 ManagerAction_QueueLog
            Asterisk 14 ManagerAction_QueueMemberRingInUse
            Asterisk 14 ManagerAction_QueuePause
            Asterisk 14 ManagerAction_QueuePenalty
            Asterisk 14 ManagerAction_QueueReload
            Asterisk 14 ManagerAction_QueueRemove
            Asterisk 14 ManagerAction_QueueReset
            Asterisk 14 ManagerAction_QueueRule
            Asterisk 14 ManagerAction_Queues
            Asterisk 14 ManagerAction_QueueStatus
            Asterisk 14 ManagerAction_QueueSummary
            Asterisk 14 ManagerAction_Redirect
            Asterisk 14 ManagerAction_Reload
            Asterisk 14 ManagerAction_SendText
            Asterisk 14 ManagerAction_Setvar
            Asterisk 14 ManagerAction_ShowDialPlan
            Asterisk 14 ManagerAction_SIPnotify
            Asterisk 14 ManagerAction_SIPpeers
            Asterisk 14 ManagerAction_SIPpeerstatus
            Asterisk 14 ManagerAction_SIPqualifypeer
            Asterisk 14 ManagerAction_SIPshowpeer
            Asterisk 14 ManagerAction_SIPshowregistry
            Asterisk 14 ManagerAction_SKINNYdevices
            Asterisk 14 ManagerAction_SKINNYlines
            Asterisk 14 ManagerAction_SKINNYshowdevice
            Asterisk 14 ManagerAction_SKINNYshowline
            Asterisk 14 ManagerAction_SorceryMemoryCacheExpire
            Asterisk 14 ManagerAction_SorceryMemoryCacheExpireObject
            Asterisk 14 ManagerAction_SorceryMemoryCachePopulate
            Asterisk 14 ManagerAction_SorceryMemoryCacheStale
            Asterisk 14 ManagerAction_SorceryMemoryCacheStaleObject
            Asterisk 14 ManagerAction_Status
            Asterisk 14 ManagerAction_StopMixMonitor
            Asterisk 14 ManagerAction_StopMonitor
            Asterisk 14 ManagerAction_UnpauseMonitor
            Asterisk 14 ManagerAction_UpdateConfig
            Asterisk 14 ManagerAction_UserEvent
            Asterisk 14 ManagerAction_VoicemailRefresh
            Asterisk 14 ManagerAction_VoicemailUsersList
            Asterisk 14 ManagerAction_WaitEvent
        Asterisk 14 AMI Events
            Asterisk 14 ManagerEvent_AgentCalled
            Asterisk 14 ManagerEvent_AgentComplete
            Asterisk 14 ManagerEvent_AgentConnect
            Asterisk 14 ManagerEvent_AgentDump
            Asterisk 14 ManagerEvent_AgentLogin
            Asterisk 14 ManagerEvent_AgentLogoff
            Asterisk 14 ManagerEvent_AgentRingNoAnswer
            Asterisk 14 ManagerEvent_Agents
            Asterisk 14 ManagerEvent_AgentsComplete
            Asterisk 14 ManagerEvent_AGIExecEnd
            Asterisk 14 ManagerEvent_AGIExecStart
            Asterisk 14 ManagerEvent_Alarm
            Asterisk 14 ManagerEvent_AlarmClear
            Asterisk 14 ManagerEvent_AOC-D
            Asterisk 14 ManagerEvent_AOC-E
            Asterisk 14 ManagerEvent_AOC-S
            Asterisk 14 ManagerEvent_AorDetail
            Asterisk 14 ManagerEvent_AsyncAGIEnd
            Asterisk 14 ManagerEvent_AsyncAGIExec
            Asterisk 14 ManagerEvent_AsyncAGIStart
            Asterisk 14 ManagerEvent_AttendedTransfer
            Asterisk 14 ManagerEvent_AuthDetail
            Asterisk 14 ManagerEvent_AuthMethodNotAllowed
            Asterisk 14 ManagerEvent_BlindTransfer
            Asterisk 14 ManagerEvent_BridgeCreate
            Asterisk 14 ManagerEvent_BridgeDestroy
            Asterisk 14 ManagerEvent_BridgeEnter
            Asterisk 14 ManagerEvent_BridgeInfoChannel
            Asterisk 14 ManagerEvent_BridgeInfoComplete
            Asterisk 14 ManagerEvent_BridgeLeave
            Asterisk 14 ManagerEvent_BridgeMerge
            Asterisk 14 ManagerEvent_Cdr
            Asterisk 14 ManagerEvent_CEL
            Asterisk 14 ManagerEvent_ChallengeResponseFailed
            Asterisk 14 ManagerEvent_ChallengeSent
            Asterisk 14 ManagerEvent_ChannelTalkingStart
            Asterisk 14 ManagerEvent_ChannelTalkingStop
            Asterisk 14 ManagerEvent_ChanSpyStart
            Asterisk 14 ManagerEvent_ChanSpyStop
            Asterisk 14 ManagerEvent_ConfbridgeEnd
            Asterisk 14 ManagerEvent_ConfbridgeJoin
            Asterisk 14 ManagerEvent_ConfbridgeLeave
            Asterisk 14 ManagerEvent_ConfbridgeMute
            Asterisk 14 ManagerEvent_ConfbridgeRecord
            Asterisk 14 ManagerEvent_ConfbridgeStart
            Asterisk 14 ManagerEvent_ConfbridgeStopRecord
            Asterisk 14 ManagerEvent_ConfbridgeTalking
            Asterisk 14 ManagerEvent_ConfbridgeUnmute
            Asterisk 14 ManagerEvent_ContactStatus
            Asterisk 14 ManagerEvent_ContactStatusDetail
            Asterisk 14 ManagerEvent_CoreShowChannel
            Asterisk 14 ManagerEvent_CoreShowChannelsComplete
            Asterisk 14 ManagerEvent_DAHDIChannel
            Asterisk 14 ManagerEvent_DeviceStateChange
            Asterisk 14 ManagerEvent_DeviceStateListComplete
            Asterisk 14 ManagerEvent_DialBegin
            Asterisk 14 ManagerEvent_DialEnd
            Asterisk 14 ManagerEvent_DialState
            Asterisk 14 ManagerEvent_DNDState
            Asterisk 14 ManagerEvent_DTMFBegin
            Asterisk 14 ManagerEvent_DTMFEnd
            Asterisk 14 ManagerEvent_EndpointDetail
            Asterisk 14 ManagerEvent_EndpointDetailComplete
            Asterisk 14 ManagerEvent_EndpointList
            Asterisk 14 ManagerEvent_EndpointListComplete
            Asterisk 14 ManagerEvent_ExtensionStateListComplete
            Asterisk 14 ManagerEvent_ExtensionStatus
            Asterisk 14 ManagerEvent_FailedACL
            Asterisk 14 ManagerEvent_FAXSession
            Asterisk 14 ManagerEvent_FAXSessionsComplete
            Asterisk 14 ManagerEvent_FAXSessionsEntry
            Asterisk 14 ManagerEvent_FAXStats
            Asterisk 14 ManagerEvent_FAXStatus
            Asterisk 14 ManagerEvent_FullyBooted
            Asterisk 14 ManagerEvent_Hangup
            Asterisk 14 ManagerEvent_HangupHandlerPop
            Asterisk 14 ManagerEvent_HangupHandlerPush
            Asterisk 14 ManagerEvent_HangupHandlerRun
            Asterisk 14 ManagerEvent_HangupRequest
            Asterisk 14 ManagerEvent_Hold
            Asterisk 14 ManagerEvent_IdentifyDetail
            Asterisk 14 ManagerEvent_InvalidAccountID
            Asterisk 14 ManagerEvent_InvalidPassword
            Asterisk 14 ManagerEvent_InvalidTransport
            Asterisk 14 ManagerEvent_LoadAverageLimit
            Asterisk 14 ManagerEvent_LocalBridge
            Asterisk 14 ManagerEvent_LocalOptimizationBegin
            Asterisk 14 ManagerEvent_LocalOptimizationEnd
            Asterisk 14 ManagerEvent_LogChannel
            Asterisk 14 ManagerEvent_MCID
            Asterisk 14 ManagerEvent_MeetmeEnd
            Asterisk 14 ManagerEvent_MeetmeJoin
            Asterisk 14 ManagerEvent_MeetmeLeave
            Asterisk 14 ManagerEvent_MeetmeMute
            Asterisk 14 ManagerEvent_MeetmeTalking
            Asterisk 14 ManagerEvent_MeetmeTalkRequest
            Asterisk 14 ManagerEvent_MemoryLimit
            Asterisk 14 ManagerEvent_MessageWaiting
            Asterisk 14 ManagerEvent_MiniVoiceMail
            Asterisk 14 ManagerEvent_MonitorStart
            Asterisk 14 ManagerEvent_MonitorStop
            Asterisk 14 ManagerEvent_MusicOnHoldStart
            Asterisk 14 ManagerEvent_MusicOnHoldStop
            Asterisk 14 ManagerEvent_MWIGet
            Asterisk 14 ManagerEvent_MWIGetComplete
            Asterisk 14 ManagerEvent_NewAccountCode
            Asterisk 14 ManagerEvent_NewCallerid
            Asterisk 14 ManagerEvent_Newchannel
            Asterisk 14 ManagerEvent_NewExten
            Asterisk 14 ManagerEvent_Newstate
            Asterisk 14 ManagerEvent_OriginateResponse
            Asterisk 14 ManagerEvent_ParkedCall
            Asterisk 14 ManagerEvent_ParkedCallGiveUp
            Asterisk 14 ManagerEvent_ParkedCallSwap
            Asterisk 14 ManagerEvent_ParkedCallTimeOut
            Asterisk 14 ManagerEvent_PeerStatus
            Asterisk 14 ManagerEvent_Pickup
            Asterisk 14 ManagerEvent_PresenceStateChange
            Asterisk 14 ManagerEvent_PresenceStateListComplete
            Asterisk 14 ManagerEvent_PresenceStatus
            Asterisk 14 ManagerEvent_QueueCallerAbandon
            Asterisk 14 ManagerEvent_QueueCallerJoin
            Asterisk 14 ManagerEvent_QueueCallerLeave
            Asterisk 14 ManagerEvent_QueueMemberAdded
            Asterisk 14 ManagerEvent_QueueMemberPause
            Asterisk 14 ManagerEvent_QueueMemberPenalty
            Asterisk 14 ManagerEvent_QueueMemberRemoved
            Asterisk 14 ManagerEvent_QueueMemberRinginuse
            Asterisk 14 ManagerEvent_QueueMemberStatus
            Asterisk 14 ManagerEvent_ReceiveFAX
            Asterisk 14 ManagerEvent_Registry
            Asterisk 14 ManagerEvent_Reload
            Asterisk 14 ManagerEvent_Rename
            Asterisk 14 ManagerEvent_RequestBadFormat
            Asterisk 14 ManagerEvent_RequestNotAllowed
            Asterisk 14 ManagerEvent_RequestNotSupported
            Asterisk 14 ManagerEvent_RTCPReceived
            Asterisk 14 ManagerEvent_RTCPSent
            Asterisk 14 ManagerEvent_SendFAX
            Asterisk 14 ManagerEvent_SessionLimit
            Asterisk 14 ManagerEvent_SessionTimeout
            Asterisk 14 ManagerEvent_Shutdown
            Asterisk 14 ManagerEvent_SIPQualifyPeerDone
            Asterisk 14 ManagerEvent_SoftHangupRequest
            Asterisk 14 ManagerEvent_SpanAlarm
            Asterisk 14 ManagerEvent_SpanAlarmClear
            Asterisk 14 ManagerEvent_Status
            Asterisk 14 ManagerEvent_StatusComplete
            Asterisk 14 ManagerEvent_SuccessfulAuth
            Asterisk 14 ManagerEvent_TransportDetail
            Asterisk 14 ManagerEvent_UnexpectedAddress
            Asterisk 14 ManagerEvent_Unhold
            Asterisk 14 ManagerEvent_UnParkedCall
            Asterisk 14 ManagerEvent_UserEvent
            Asterisk 14 ManagerEvent_VarSet
        Asterisk 14 ARI
        Asterisk 14 Dialplan Applications
            Asterisk 14 Application_AddQueueMember
            Asterisk 14 Application_ADSIProg
            Asterisk 14 Application_AELSub
            Asterisk 14 Application_AgentLogin
            Asterisk 14 Application_AgentRequest
            Asterisk 14 Application_AGI
            Asterisk 14 Application_AlarmReceiver
            Asterisk 14 Application_AMD
            Asterisk 14 Application_Answer
            Asterisk 14 Application_Authenticate
            Asterisk 14 Application_BackGround
            Asterisk 14 Application_BackgroundDetect
            Asterisk 14 Application_Bridge
            Asterisk 14 Application_BridgeAdd
            Asterisk 14 Application_BridgeWait
            Asterisk 14 Application_Busy
            Asterisk 14 Application_CallCompletionCancel
            Asterisk 14 Application_CallCompletionRequest
            Asterisk 14 Application_CELGenUserEvent
            Asterisk 14 Application_ChangeMonitor
            Asterisk 14 Application_ChanIsAvail
            Asterisk 14 Application_ChannelRedirect
            Asterisk 14 Application_ChanSpy
            Asterisk 14 Application_ClearHash
            Asterisk 14 Application_ConfBridge
            Asterisk 14 Application_Congestion
            Asterisk 14 Application_ContinueWhile
            Asterisk 14 Application_ControlPlayback
            Asterisk 14 Application_DAHDIAcceptR2Call
            Asterisk 14 Application_DAHDIRAS
            Asterisk 14 Application_DAHDIScan
            Asterisk 14 Application_DAHDISendCallreroutingFacility
            Asterisk 14 Application_DAHDISendKeypadFacility
            Asterisk 14 Application_DateTime
            Asterisk 14 Application_DBdel
            Asterisk 14 Application_DBdeltree
            Asterisk 14 Application_DeadAGI
            Asterisk 14 Application_Dial
            Asterisk 14 Application_Dictate
            Asterisk 14 Application_Directory
            Asterisk 14 Application_DISA
            Asterisk 14 Application_DumpChan
            Asterisk 14 Application_EAGI
            Asterisk 14 Application_Echo
            Asterisk 14 Application_EndWhile
            Asterisk 14 Application_Exec
            Asterisk 14 Application_ExecIf
            Asterisk 14 Application_ExecIfTime
            Asterisk 14 Application_ExitWhile
            Asterisk 14 Application_ExtenSpy
            Asterisk 14 Application_ExternalIVR
            Asterisk 14 Application_Festival
            Asterisk 14 Application_Flash
            Asterisk 14 Application_FollowMe
            Asterisk 14 Application_ForkCDR
            Asterisk 14 Application_GetCPEID
            Asterisk 14 Application_Gosub
            Asterisk 14 Application_GosubIf
            Asterisk 14 Application_Goto
            Asterisk 14 Application_GotoIf
            Asterisk 14 Application_GotoIfTime
            Asterisk 14 Application_Hangup
            Asterisk 14 Application_HangupCauseClear
            Asterisk 14 Application_IAX2Provision
            Asterisk 14 Application_ICES
            Asterisk 14 Application_ImportVar
            Asterisk 14 Application_Incomplete
            Asterisk 14 Application_IVRDemo
            Asterisk 14 Application_JabberJoin_res_xmpp
            Asterisk 14 Application_JabberLeave_res_xmpp
            Asterisk 14 Application_JabberSend_res_xmpp
            Asterisk 14 Application_JabberSendGroup_res_xmpp
            Asterisk 14 Application_JabberStatus_res_xmpp
            Asterisk 14 Application_JACK
            Asterisk 14 Application_Log
            Asterisk 14 Application_Macro
            Asterisk 14 Application_MacroExclusive
            Asterisk 14 Application_MacroExit
            Asterisk 14 Application_MacroIf
            Asterisk 14 Application_MailboxExists
            Asterisk 14 Application_MeetMe
            Asterisk 14 Application_MeetMeAdmin
            Asterisk 14 Application_MeetMeChannelAdmin
            Asterisk 14 Application_MeetMeCount
            Asterisk 14 Application_MessageSend
            Asterisk 14 Application_Milliwatt
            Asterisk 14 Application_MinivmAccMess
            Asterisk 14 Application_MinivmDelete
            Asterisk 14 Application_MinivmGreet
            Asterisk 14 Application_MinivmMWI
            Asterisk 14 Application_MinivmNotify
            Asterisk 14 Application_MinivmRecord
            Asterisk 14 Application_MixMonitor
            Asterisk 14 Application_Monitor
            Asterisk 14 Application_Morsecode
            Asterisk 14 Application_MP3Player
            Asterisk 14 Application_MSet
            Asterisk 14 Application_MusicOnHold
            Asterisk 14 Application_NBScat
            Asterisk 14 Application_NoCDR
            Asterisk 14 Application_NoOp
            Asterisk 14 Application_ODBC_Commit
            Asterisk 14 Application_ODBC_Rollback
            Asterisk 14 Application_ODBCFinish
            Asterisk 14 Application_Originate
            Asterisk 14 Application_OSPAuth
            Asterisk 14 Application_OSPFinish
            Asterisk 14 Application_OSPLookup
            Asterisk 14 Application_OSPNext
            Asterisk 14 Application_Page
            Asterisk 14 Application_Park
            Asterisk 14 Application_ParkAndAnnounce
            Asterisk 14 Application_ParkedCall
            Asterisk 14 Application_PauseMonitor
            Asterisk 14 Application_PauseQueueMember
            Asterisk 14 Application_Pickup
            Asterisk 14 Application_PickupChan
            Asterisk 14 Application_Playback
            Asterisk 14 Application_PlayTones
            Asterisk 14 Application_PrivacyManager
            Asterisk 14 Application_Proceeding
            Asterisk 14 Application_Progress
            Asterisk 14 Application_Queue
            Asterisk 14 Application_QueueLog
            Asterisk 14 Application_RaiseException
            Asterisk 14 Application_Read
            Asterisk 14 Application_ReadExten
            Asterisk 14 Application_ReceiveFAX_app_fax
            Asterisk 14 Application_ReceiveFAX_res_fax
            Asterisk 14 Application_Record
            Asterisk 14 Application_RemoveQueueMember
            Asterisk 14 Application_ResetCDR
            Asterisk 14 Application_RetryDial
            Asterisk 14 Application_Return
            Asterisk 14 Application_Ringing
            Asterisk 14 Application_SayAlpha
            Asterisk 14 Application_SayAlphaCase
            Asterisk 14 Application_SayCountedAdj
            Asterisk 14 Application_SayCountedNoun
            Asterisk 14 Application_SayDigits
            Asterisk 14 Application_SayNumber
            Asterisk 14 Application_SayPhonetic
            Asterisk 14 Application_SayUnixTime
            Asterisk 14 Application_SendDTMF
            Asterisk 14 Application_SendFAX_app_fax
            Asterisk 14 Application_SendFAX_res_fax
            Asterisk 14 Application_SendImage
            Asterisk 14 Application_SendText
            Asterisk 14 Application_SendURL
            Asterisk 14 Application_Set
            Asterisk 14 Application_SetAMAFlags
            Asterisk 14 Application_SetCallerPres
            Asterisk 14 Application_SIPAddHeader
            Asterisk 14 Application_SIPDtmfMode
            Asterisk 14 Application_SIPRemoveHeader
            Asterisk 14 Application_SIPSendCustomINFO
            Asterisk 14 Application_SkelGuessNumber
            Asterisk 14 Application_SLAStation
            Asterisk 14 Application_SLATrunk
            Asterisk 14 Application_SMS
            Asterisk 14 Application_SoftHangup
            Asterisk 14 Application_SpeechActivateGrammar
            Asterisk 14 Application_SpeechBackground
            Asterisk 14 Application_SpeechCreate
            Asterisk 14 Application_SpeechDeactivateGrammar
            Asterisk 14 Application_SpeechDestroy
            Asterisk 14 Application_SpeechLoadGrammar
            Asterisk 14 Application_SpeechProcessingSound
            Asterisk 14 Application_SpeechStart
            Asterisk 14 Application_SpeechUnloadGrammar
            Asterisk 14 Application_StackPop
            Asterisk 14 Application_StartMusicOnHold
            Asterisk 14 Application_Stasis
            Asterisk 14 Application_StatsD
            Asterisk 14 Application_StopMixMonitor
            Asterisk 14 Application_StopMonitor
            Asterisk 14 Application_StopMusicOnHold
            Asterisk 14 Application_StopPlayTones
            Asterisk 14 Application_System
            Asterisk 14 Application_TestClient
            Asterisk 14 Application_TestServer
            Asterisk 14 Application_Transfer
            Asterisk 14 Application_TryExec
            Asterisk 14 Application_TrySystem
            Asterisk 14 Application_UnpauseMonitor
            Asterisk 14 Application_UnpauseQueueMember
            Asterisk 14 Application_UserEvent
            Asterisk 14 Application_Verbose
            Asterisk 14 Application_VMAuthenticate
            Asterisk 14 Application_VMSayName
            Asterisk 14 Application_VoiceMail
            Asterisk 14 Application_VoiceMailMain
            Asterisk 14 Application_VoiceMailPlayMsg
            Asterisk 14 Application_Wait
            Asterisk 14 Application_WaitExten
            Asterisk 14 Application_WaitForNoise
            Asterisk 14 Application_WaitForRing
            Asterisk 14 Application_WaitForSilence
            Asterisk 14 Application_WaitUntil
            Asterisk 14 Application_While
            Asterisk 14 Application_Zapateller
        Asterisk 14 Dialplan Functions
            Asterisk 14 Function_AES_DECRYPT
            Asterisk 14 Function_AES_ENCRYPT
            Asterisk 14 Function_AGC
            Asterisk 14 Function_AGENT
            Asterisk 14 Function_AMI_CLIENT
            Asterisk 14 Function_ARRAY
            Asterisk 14 Function_AST_CONFIG
            Asterisk 14 Function_AST_SORCERY
            Asterisk 14 Function_AUDIOHOOK_INHERIT
            Asterisk 14 Function_BASE64_DECODE
            Asterisk 14 Function_BASE64_ENCODE
            Asterisk 14 Function_BLACKLIST
            Asterisk 14 Function_CALENDAR_BUSY
            Asterisk 14 Function_CALENDAR_EVENT
            Asterisk 14 Function_CALENDAR_QUERY
            Asterisk 14 Function_CALENDAR_QUERY_RESULT
            Asterisk 14 Function_CALENDAR_WRITE
            Asterisk 14 Function_CALLCOMPLETION
            Asterisk 14 Function_CALLERID
            Asterisk 14 Function_CALLERPRES
            Asterisk 14 Function_CDR
            Asterisk 14 Function_CDR_PROP
            Asterisk 14 Function_CHANNEL
            Asterisk 14 Function_CHANNELS
            Asterisk 14 Function_CHECKSIPDOMAIN
            Asterisk 14 Function_CONFBRIDGE
            Asterisk 14 Function_CONFBRIDGE_INFO
            Asterisk 14 Function_CONNECTEDLINE
            Asterisk 14 Function_CSV_QUOTE
            Asterisk 14 Function_CURL
            Asterisk 14 Function_CURLOPT
            Asterisk 14 Function_CUT
            Asterisk 14 Function_DB
            Asterisk 14 Function_DB_DELETE
            Asterisk 14 Function_DB_EXISTS
            Asterisk 14 Function_DB_KEYS
            Asterisk 14 Function_DEC
            Asterisk 14 Function_DENOISE
            Asterisk 14 Function_DEVICE_STATE
            Asterisk 14 Function_DIALGROUP
            Asterisk 14 Function_DIALPLAN_EXISTS
            Asterisk 14 Function_DUNDILOOKUP
            Asterisk 14 Function_DUNDIQUERY
            Asterisk 14 Function_DUNDIRESULT
            Asterisk 14 Function_ENUMLOOKUP
            Asterisk 14 Function_ENUMQUERY
            Asterisk 14 Function_ENUMRESULT
            Asterisk 14 Function_ENV
            Asterisk 14 Function_EVAL
            Asterisk 14 Function_EXCEPTION
            Asterisk 14 Function_EXISTS
            Asterisk 14 Function_EXTENSION_STATE
            Asterisk 14 Function_FAXOPT_res_fax
            Asterisk 14 Function_FEATURE
            Asterisk 14 Function_FEATUREMAP
            Asterisk 14 Function_FIELDNUM
            Asterisk 14 Function_FIELDQTY
            Asterisk 14 Function_FILE
            Asterisk 14 Function_FILE_COUNT_LINE
            Asterisk 14 Function_FILE_FORMAT
            Asterisk 14 Function_FILTER
            Asterisk 14 Function_FRAME_TRACE
            Asterisk 14 Function_GLOBAL
            Asterisk 14 Function_GROUP
            Asterisk 14 Function_GROUP_COUNT
            Asterisk 14 Function_GROUP_LIST
            Asterisk 14 Function_GROUP_MATCH_COUNT
            Asterisk 14 Function_HANGUPCAUSE
            Asterisk 14 Function_HANGUPCAUSE_KEYS
            Asterisk 14 Function_HASH
            Asterisk 14 Function_HASHKEYS
            Asterisk 14 Function_HINT
            Asterisk 14 Function_HOLD_INTERCEPT
            Asterisk 14 Function_IAXPEER
            Asterisk 14 Function_IAXVAR
            Asterisk 14 Function_ICONV
            Asterisk 14 Function_IF
            Asterisk 14 Function_IFMODULE
            Asterisk 14 Function_IFTIME
            Asterisk 14 Function_IMPORT
            Asterisk 14 Function_INC
            Asterisk 14 Function_ISNULL
            Asterisk 14 Function_JABBER_RECEIVE_res_xmpp
            Asterisk 14 Function_JABBER_STATUS_res_xmpp
            Asterisk 14 Function_JITTERBUFFER
            Asterisk 14 Function_KEYPADHASH
            Asterisk 14 Function_LEN
            Asterisk 14 Function_LISTFILTER
            Asterisk 14 Function_LOCAL
            Asterisk 14 Function_LOCAL_PEEK
            Asterisk 14 Function_LOCK
            Asterisk 14 Function_MAILBOX_EXISTS
            Asterisk 14 Function_MASTER_CHANNEL
            Asterisk 14 Function_MATH
            Asterisk 14 Function_MD5
            Asterisk 14 Function_MEETME_INFO
            Asterisk 14 Function_MESSAGE
            Asterisk 14 Function_MESSAGE_DATA
            Asterisk 14 Function_MINIVMACCOUNT
            Asterisk 14 Function_MINIVMCOUNTER
            Asterisk 14 Function_MIXMONITOR
            Asterisk 14 Function_MUTEAUDIO
            Asterisk 14 Function_ODBC
            Asterisk 14 Function_ODBC_FETCH
            Asterisk 14 Function_PASSTHRU
            Asterisk 14 Function_PERIODIC_HOOK
            Asterisk 14 Function_PITCH_SHIFT
            Asterisk 14 Function_PJSIP_AOR
            Asterisk 14 Function_PJSIP_CONTACT
            Asterisk 14 Function_PJSIP_DIAL_CONTACTS
            Asterisk 14 Function_PJSIP_ENDPOINT
            Asterisk 14 Function_PJSIP_HEADER
            Asterisk 14 Function_PJSIP_MEDIA_OFFER
            Asterisk 14 Function_POP
            Asterisk 14 Function_PP_EACH_EXTENSION
            Asterisk 14 Function_PP_EACH_USER
            Asterisk 14 Function_PRESENCE_STATE
            Asterisk 14 Function_PUSH
            Asterisk 14 Function_QUEUE_EXISTS
            Asterisk 14 Function_QUEUE_GET_CHANNEL
            Asterisk 14 Function_QUEUE_MEMBER
            Asterisk 14 Function_QUEUE_MEMBER_COUNT
            Asterisk 14 Function_QUEUE_MEMBER_LIST
            Asterisk 14 Function_QUEUE_MEMBER_PENALTY
            Asterisk 14 Function_QUEUE_VARIABLES
            Asterisk 14 Function_QUEUE_WAITING_COUNT
            Asterisk 14 Function_QUOTE
            Asterisk 14 Function_RAND
            Asterisk 14 Function_REALTIME
            Asterisk 14 Function_REALTIME_DESTROY
            Asterisk 14 Function_REALTIME_FIELD
            Asterisk 14 Function_REALTIME_HASH
            Asterisk 14 Function_REALTIME_STORE
            Asterisk 14 Function_REDIRECTING
            Asterisk 14 Function_REGEX
            Asterisk 14 Function_REPLACE
            Asterisk 14 Function_SET
            Asterisk 14 Function_SHA1
            Asterisk 14 Function_SHARED
            Asterisk 14 Function_SHELL
            Asterisk 14 Function_SHIFT
            Asterisk 14 Function_SIP_HEADER
            Asterisk 14 Function_SIPPEER
            Asterisk 14 Function_SMDI_MSG
            Asterisk 14 Function_SMDI_MSG_RETRIEVE
            Asterisk 14 Function_SORT
            Asterisk 14 Function_SPEECH
            Asterisk 14 Function_SPEECH_ENGINE
            Asterisk 14 Function_SPEECH_GRAMMAR
            Asterisk 14 Function_SPEECH_RESULTS_TYPE
            Asterisk 14 Function_SPEECH_SCORE
            Asterisk 14 Function_SPEECH_TEXT
            Asterisk 14 Function_SPRINTF
            Asterisk 14 Function_SQL_ESC
            Asterisk 14 Function_SRVQUERY
            Asterisk 14 Function_SRVRESULT
            Asterisk 14 Function_STACK_PEEK
            Asterisk 14 Function_STAT
            Asterisk 14 Function_STRFTIME
            Asterisk 14 Function_STRPTIME
            Asterisk 14 Function_STRREPLACE
            Asterisk 14 Function_SYSINFO
            Asterisk 14 Function_TALK_DETECT
            Asterisk 14 Function_TESTTIME
            Asterisk 14 Function_TIMEOUT
            Asterisk 14 Function_TOLOWER
            Asterisk 14 Function_TOUPPER
            Asterisk 14 Function_TRYLOCK
            Asterisk 14 Function_TXTCIDNAME
            Asterisk 14 Function_UNLOCK
            Asterisk 14 Function_UNSHIFT
            Asterisk 14 Function_URIDECODE
            Asterisk 14 Function_URIENCODE
            Asterisk 14 Function_VALID_EXTEN
            Asterisk 14 Function_VERSION
            Asterisk 14 Function_VM_INFO
            Asterisk 14 Function_VMCOUNT
            Asterisk 14 Function_VOLUME
        Asterisk 14 Module Configuration
            Asterisk 14 Configuration_app_agent_pool
            Asterisk 14 Configuration_app_confbridge
            Asterisk 14 Configuration_app_skel
            Asterisk 14 Configuration_cdr
            Asterisk 14 Configuration_cel
            Asterisk 14 Configuration_chan_motif
            Asterisk 14 Configuration_core
            Asterisk 14 Configuration_features
            Asterisk 14 Configuration_named_acl
            Asterisk 14 Configuration_res_ari
            Asterisk 14 Configuration_res_hep
            Asterisk 14 Configuration_res_mwi_external
            Asterisk 14 Configuration_res_parking
            Asterisk 14 Configuration_res_pjproject
            Asterisk 14 Configuration_res_pjsip
            Asterisk 14 Configuration_res_pjsip_acl
            Asterisk 14 Configuration_res_pjsip_config_wizard
            Asterisk 14 Configuration_res_pjsip_endpoint_identifier_ip
            Asterisk 14 Configuration_res_pjsip_notify
            Asterisk 14 Configuration_res_pjsip_outbound_publish
            Asterisk 14 Configuration_res_pjsip_outbound_registration
            Asterisk 14 Configuration_res_pjsip_phoneprov_provider
            Asterisk 14 Configuration_res_pjsip_publish_asterisk
            Asterisk 14 Configuration_res_pjsip_pubsub
            Asterisk 14 Configuration_res_resolver_unbound
            Asterisk 14 Configuration_res_statsd
            Asterisk 14 Configuration_res_xmpp
            Asterisk 14 Configuration_stasis
            Asterisk 14 Configuration_udptl
