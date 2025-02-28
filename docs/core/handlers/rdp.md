# Remote Desktop Protocol (RDP) Configuration

???+ info "Sample Configuration"
    The sample configuration below is also available in the [GHOSTS GitHub repository](<https://github.com/cmu-sei/GHOSTS/blob/master/src/Ghosts.Client/Sample%20Timelines/clicks>

Each CommandArg is of the form shown below, if multiple CommandArgs are present a random one is chosen for execution on each cycle.

- `targetIp`|`credkey`  The targetIP is the IP to use for the RDP connection
- The `credKey` is only used to retrieve the password of the matching record in the credentials file.
- The username (if supplied) is  used instead of the logged-in user (can also provide 'domain' keyword in credentials)
- The password is used if a password  prompt appears on RDP open


```json
{
  "Status": "Run",
  "TimeLineHandlers": [
    {
      "HandlerType": "Rdp",
      "HandlerArgs": {
        "CredentialsFile": "<path to credentials>", //required, file path to a JSON file containing the RDP credentials
        "mouse-sleep-time": 10000, //time to sleep between random mouse movements
        "execution-time": 60000, //after this total connection time has elapsed, the RDP is closed and a new connection opened
        "execution-probability": 100, //after choosing a random target, the probability that a RDP to the target is opened
        "delay-jitter": 50

      },
      "Initial": "",
      "UtcTimeOn": "00:00:00",
      "UtcTimeOff": "24:00:00",
      "Loop": "True",
      "TimeLineEvents": [
        {
          "Command": "random",
          "CommandArgs": [
            "<targetIp>|<credkey>"
          ],
          "DelayAfter": 20000,
          "DelayBefore": 0
        }
      ]
    }


  ]
}
```
