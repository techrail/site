---
draft: false
title: Parsing log strings in Bark
tags:
  - blog
  - vaibhav
  - bark
---
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

