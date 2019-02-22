### [6.1.2 RTCSctpTransportState Enum](http://w3c.github.io/webrtc-pc/#rtcsctptransportstate)

RTCSctpTransportState indicates the state of the SCTP transport.

zh:RTCSctpTransportState指示SCTP传输的状态。

```
enum RTCSctpTransportState {
    "connecting",
    "connected",
    "closed"
};
```
<table>
	<tr>
		<td colspan="2">
		Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		connecting
		</td>
		<td>
		The RTCSctpTransport is in the process of negotiating an association. This is the initial state of the [[SctpTransportState]] slot when an RTCSctpTransport is created.
		</td>
	</tr>
	<tr>
		<td>
		connected
		</td>
		<td>
		When the negotiation of an association is completed, a task is queued to update the [[SctpTransportState]] slot to "connected".
		</td>
	</tr>
	<tr>
		<td>
		closed
		</td>
		<td>
		A task is queued to update the [[SctpTransportState]] slot to "closed" when a SHUTDOWN or ABORT chunk is received or when the SCTP association has been closed intentionally, such as by closing the peer connection or applying a remote description that rejects data or changes the SCTP port.
		</td>
	</tr>
</table>
