# Metasploit Constants

## Exploit Check Codes

[Source File](https://github.com/rapid7/metasploit-framework/blob/master/lib/msf/core/exploit.rb)

| Constant Name          | Constant Description                                       |
|:-----------------------|:-----------------------------------------------------------|
| CheckCode::Unknown     | Cannot reliably check exploitability.                      |
| CheckCode::Safe        | The target is not exploitable.                             |
| CheckCode::Detected    | The target service is running, but could not be validated. |
| CheckCode::Appears     | The target appears to be vulnerable.                       |
| CheckCode::Vulnerable  | The target is vulnerable.                                  |
| CheckCode::Unsupported | This module does not support check.                        |

## Exploit Module Rankings

[Source File](https://github.com/rapid7/metasploit-framework/blob/master/lib/msf/core/constants.rb)
[More Details](https://github.com/rapid7/metasploit-framework/wiki/Exploit-Ranking)

| Constant Name    | Constant Description |
|:-----------------|:---------------------|
| ExcellentRanking | The exploit will never crash the service. This is the case for SQL Injection, CMD execution, RFI, LFI, etc. No typical memory corruption exploits should be given this ranking unless there are extraordinary circumstances (WMF Escape()). |
| GreatRanking     | The exploit has a default target AND either auto-detects the appropriate target or uses an application-specific return address AFTER a version check. |
| GoodRanking      | The exploit has a default target and it is the "common case" for this type of software (English, Windows XP for a desktop app, 2003 for server, etc). |
| NormalRanking    | The exploit is otherwise reliable, but depends on a specific version and can't (or doesn't) reliably autodetect. |
| AverageRanking   | The exploit is generally unreliable or difficult to exploit. |
| LowRanking       | The exploit is nearly impossible to exploit (or under 50%) for common platforms. |
| ManualRanking    | The exploit is unstable or difficult to exploit and is basically a DoS. This ranking is also used when the module has no use unless specifically configured by the user (e.g.: php_eval). |

## Module Failure Statuses

[Source File](https://github.com/rapid7/metasploit-framework/blob/master/lib/msf/core/module.rb)

| Constant Name            | Constant Description                                                   |
|:-------------------------|:-----------------------------------------------------------------------|
| Failure::BadConfig       | The exploit settings were incorrect                                    |
| Failure::Disconnected    | The network service disconnected us mid-attempt                        |
| Failure::NoAccess        | The application replied indication we do not have access               |
| Failure::None            | No confidence in success or failure                                    |
| Failure::NoTarget        | The target is not compatible with this exploit or settings             |
| Failure::NotFound        | The application endpoint or specific service was not found             |
| Failure::NotVulnerable   | The application response indicated it was not vulnerable               |
| Failure::PayloadFailed   | The payload was delivered but no session was opened (AV, network, etc) |
| Failure::TimeoutExpired  | The exploit triggered some form of timeout                             |
| Failure::UnexpectedReply | The application replied in an unexpected fashion                       |
| Failure::Unknown         | No confidence in success or failure                                    |
| Failure::Unreachable     | The network service was unreachable (connection refused, etc)          |
| Failure::UserInterrupt   | The exploit was interrupted by the user                                |
