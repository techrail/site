---
draft: true
title: Parsing log strings in Bark
tags:
  - blog
  - vaibhav
  - bark
---
Bark contains a client library which can be imported in a Golang project. Now, logs in bark are actually structured. They have a Level, a [[logging-errors-properly|LMID]] and the actual message. So we wrote a parser which tries parse the log message and if it fits the formats, it would set the level and LMID along with the Log message. 

## The Format and Behaviour
The general format of the Log message which the parser understands (and expects) is like this: 

```
<LVL_CHAR>#<LMID> - <LOG_MESSAGE>
```

In this format:

1. `LVL_CHAR`: is a _single character_ indicating the log level. The accepted characters are basically the first character of their names:
	- `P`: Panic
	- `A`: Alert
	- `E`: Error
	- `W`: Warning
	- `N`: Notice
	- `I`: Info
	- `D`: Debug
	- Anything else will automatically be set to the default log level set by the user when creating the client
1. `LMID`: Is the Log Message Identifier. It is separated on the left from `LVL_CHAR` by a `#` and on the right from the `LOG_MESSAGE` by a ` - `. The spaces around `-` are optional but recommended to be left as it is.
2. `LOG_MESSAGE`: This is the actual Log Message which the user wants to save.


## Examples

Here is how it behaves: 

| String sent                                       | Level    | Log Message ID | Log message                                       |
| ------------------------------------------------- | -------- | -------------- | ------------------------------------------------- |
| `D#LMID1 - Log message`                           | `DEBUG`  | `LMID1`        | `Log message`                                     |
| `I#LMID2 - Log message2`                          | `INFO`   | `LMID2`        | `Log message2`                                    |
| `N#LMID3 - Log message3`                          | `NOTICE` | `LMID3`        | `Log message3`                                    |
| `W#LMID4 - Log message4`                          | `WARN`   | `LMID4`        | `Log message4`                                    |
| `E#LMID5 - Log message5`                          | `ERROR`  | `LMID5`        | `Log message5`                                    |
| `A#LMID6 - Log message6`                          | `ALERT`  | `LMID6`        | `Log message6`                                    |
| `P#LMID7 - Log message7`                          | `ERROR`  | `LMID7`        | `Log message7`                                    |
| `LMID2 - Log message8`                            | `INFO`   | `LMID2`        | `Log message8`                                    |
| `Log message9`                                    | `INFO`   | `000000`       | `Log message9`                                    |
| `- Log message10`                                 | `INFO`   | `000000`       | `- Log message10`                                 |
| ` # - Log message11`                              | `INFO`   | `000000`       | ` # - Log message11`                              |
| `X# - Log message12`                              | `INFO`   | `000000`       | `X# - Log message12`                              |
| `XX# - Log message13`                             | `INFO`   | `000000`       | `XX# - Log message13`                             |
| `XX#LMID14 - Log message14`                       | `INFO`   | `000000`       | `XX#LMID14 - Log message14`                       |
| `XX#LMIDINTHISCASEISVERYVERYLONG - Log message15` | `INFO`   | `000000`       | `XX#LMIDINTHISCASEISVERYVERYLONG - Log message15` |
| `#LMIDINTHISCASEISVERYVERYLONG - Log message16`   | `INFO`   | `000000`       | `#LMIDINTHISCASEISVERYVERYLONG - Log message16`   |
| `#LMID17 - Log message17`                         | `INFO`   | `000000`       | `#LMID17 - Log message17`                         |
| `D#LMID18 - Log message18`                        | `DEBUG`  | `LMID18`       | `Log message18`                                   |

