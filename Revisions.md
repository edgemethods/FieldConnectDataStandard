# Revisions

Spec | Date      | Notes
---- | --------- | -----
0.9	| 2 June 2016 |	Final draft
0.9.2 |	3 October 2016 | Adjustments
0.9.3 |	27 December 2016 | Renamed DeviceIdentifier to DeviceId and ComponentId to ComponentCode
0.9.4 |	5 January 2017 | Added privacy property
0.9.5 |	23 January 2017	| Added adjustments property
0.9.6.0 | 28 February 2017 | Extensive updates. Added ComponentCycleMessage, added IntervalEventMessage, removed most derived messages
0.9.6.1	| 20 March 2017 | Added OperationMessage
0.9.7.0	| 28 March 2017	| Added ‘Tags’
0.9.7.1	| 11 April 2017	| Renamed "ComponentsMessage" to "ComponentConfigurationMessage" and added SerialNumber
0.9.8.0	| 1 June 2017 |	Updated FileUploadMessgae. Added server-side validations. Notes update on Component Cycle Message. Removed Component State Message. Changed Basic Diagnostic Message to key-value store. Added samples for ErrorsMessage, CommandResponseMessage, BasicDiagnosticMessage. Added ManualLocation to MachineLocationMessage. Clarified DateTime format. Updated UnexpectedStateMessage. Added Unexpected Component Message.
0.9.8.1	| 16 June 2017 | Added Tags to "ComponentConfigurationMessage"
0.9.9.0	| 23 October 2017 |	Added [Spec] and removed [Contract]
0.9.9.1	| 6 November 2017 |	Added EntityTagMessage
0.9.9.2	| 23 November 2017 | Added "HighImportance" property
1.0.0.0	| 12 December 2017 | On ComponentConfigurationMessage, removed [Tags] and added [Properties]. Added [PartNumber]
1.0.1.0	| 18 December 2017 | Added [Origin]
1.0.2.0	| 2 January 2018 | Added SuspectDeviceMessage
1.0.3.0	| 23 January 2018 |	Added CycleIdentifier to Component Cycle Message
1.1.0.0	| 30 January 2018 |	BREAKING. Changed ComponentConfigurationMessage to MachineConfigurationMessage. Added machine operation to MachineConfigurationMessage.
1.1.1.0	| 1 February 2018 |	Removed [Process] from AlertMessage. Removed [Data] from EventIntervalMessage. Added [ExecutionLog] and [CommandIdentifier] to CommandResponseMessage