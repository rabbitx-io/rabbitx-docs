---
description: >-
  Below is a detailed record of resolved and successfully paid out bug bounties,
  Each bounty includes information on time of resolution, brief description of
  the issue, its severity, and reward paid out
---

# Bug Bounty Postmortem Report



<table data-full-width="true"><thead><tr><th>Time</th><th width="303.6666259765625">Description</th><th width="96.6666259765625">Severity</th><th width="91.3331298828125">Paid out</th><th data-type="content-ref">Transaction hash</th></tr></thead><tbody><tr><td>2024-12-21</td><td> A valid signature is used to authorize ETH withdrawals, but no check is made to ensure <code>msg.sender</code> matches the intended <code>trader</code>. Attackers could  front-run transactions using the same signature to receive the funds.</td><td>High</td><td>$10,000</td><td><a href="https://etherscan.io/tx/0xea332a95e746964267b2304630fc5d19d35a8d670b1ccbc6c5d99a22cdb7f234">https://etherscan.io/tx/0xea332a95e746964267b2304630fc5d19d35a8d670b1ccbc6c5d99a22cdb7f234</a></td></tr><tr><td>2025-3-17</td><td>Click Jacking vulnerability on Wallet Connect Feature and Entire Website</td><td>Medium</td><td>$1000</td><td><a href="https://etherscan.io/tx/0x742e26aa4abbbf569f1d7fcb43adda4839c72644f7704e3cee6ba33c4c17c936">https://etherscan.io/tx/0x742e26aa4abbbf569f1d7fcb43adda4839c72644f7704e3cee6ba33c4c17c936</a></td></tr><tr><td>2025-2-24</td><td>DOS vulnerability within API implementation, which could  exhaust server capacity, leading to service disruption</td><td>Medium</td><td>$2000</td><td><a href="https://blastscan.io/tx/0xee06a01da583fe66c099e2a87840befcfec7a991bfc80e916907ae439f770097">https://blastscan.io/tx/0xee06a01da583fe66c099e2a87840befcfec7a991bfc80e916907ae439f770097</a></td></tr><tr><td>2025-3-14</td><td>Vulnerability in the API interface can cause misconfigurations in the back-end server, leading to timeouts.<br>This flaw can be exploited to crash the API interface affecting the entire Web/App platform.</td><td>Medium</td><td>$1640</td><td><a href="https://etherscan.io/tx/0x2b1729a82d1f06ee108e08c55358c456cbcdb10a007d97092f7da9ee2ce2e18c">https://etherscan.io/tx/0x2b1729a82d1f06ee108e08c55358c456cbcdb10a007d97092f7da9ee2ce2e18c</a></td></tr><tr><td></td><td></td><td></td><td></td><td></td></tr></tbody></table>

