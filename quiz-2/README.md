## CSV file format

PID, PPID, CMD

PID : Process Id

PPID: Parent Process Id

CMD : Command Line

## Example Input CSV file:

``` csv
1, 0, /sbin/launchd
2, 0, /usr/libexec/logd
3, 1, /usr/libexec/UserEventAgent (System)
4, 1, /usr/sbin/systemstats --daemon
5, 1, /usr/libexec/configd
6, 2, /usr/libexec/keybagd -t 15
7, 2, /usr/sbin/KernelEventAgent
8, 3, /usr/sbin/cfprefsd daemon
9, 3, /usr/sbin/securityd -i
10, 4, /Applications/Safari.app/Contents/MacOS/Safari
```

## Example Output JSON:

``` json
[
    {
      "pid": 1,
      "ppid": 0,
      "cmd": "/sbin/launchd",
      "children": [
        {
          "pid": 3,
          "ppid": 1,
          "cmd": "/usr/libexec/UserEventAgent (System)",
          "children": [
            {
              "pid": 8,
              "ppid": 3,
              "cmd": "/usr/sbin/cfprefsd daemon"
            },
            {
              "pid": 9,
              "ppid": 3,
              "cmd": "/usr/sbin/securityd -i"
            }
          ]
        },
        {
          "pid": 4,
          "ppid": 1,
          "cmd": "/usr/sbin/systemstats --daemon",
          "children": [
            {
              "pid": 10,
              "ppid": 4,
              "cmd": "/Applications/Safari.app/Contents/MacOS/Safari"
            }
          ]
        },
        {
          "pid": 5,
          "ppid": 1,
          "cmd": "/usr/libexec/configd"
        }
      ]
    },
    {
      "pid": 2,
      "ppid": 0,
      "cmd": "/usr/libexec/logd",
      "children": [
        {
          "pid": 6,
          "ppid": 2,
          "cmd": "/usr/libexec/keybagd -t 15"
        },
        {
          "pid": 7,
          "ppid": 2,
          "cmd": "/usr/sbin/KernelEventAgent"
        }
      ]
    }
  ]
  ```

## Note:

1. Read the CSV file from command line parameter.
1. Convert the CSV file stated as a process tree in JSON format, and print it.
1. You could verify your output with some tools, such as:

  - http://jsonviewer.stack.hu
  - https://vanya.jp.net/vtree/
