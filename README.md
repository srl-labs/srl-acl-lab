# Access Control Lists on SR Linux

Get to know ACLs on SR Linux

---
<div align=center markdown>
<a href="https://codespaces.new/srl-labs/srl-acl-lab?quickstart=1">
<img src="https://gitlab.com/rdodin/pics/-/wikis/uploads/d78a6f9f6869b3ac3c286928dd52fa08/run_in_codespaces-v1.svg?sanitize=true" style="width:50%"/></a>

**[Run](https://codespaces.new/srl-labs/srl-acl-lab?quickstart=1) this lab in GitHub Codespaces for free**.  
[Learn more](https://containerlab.dev/manual/codespaces) about Containerlab for Codespaces.  
<small>Machine type: 2 vCPU · 8 GB RAM</small>
</div>

---

After lab is started the following ping should succeed, as there is no default ACL in place.

```
sudo docker exec -i -t clab-acl-client ping -w 2 -c 2 192.168.20.100
```

Then configure the ACL on ethernet-1/1.0 subinterface of SR Linux to drop ICMP packets destined towards the server:

```bash
cat icmp_drop.cfg | docker exec -i clab-acl-srl sr_cli -e -c
```

Repeat the ping, it should not succeed, as the ICMP drop ACL is in place. You can check the logs on SR Linux to ensure that the packets are being dropped:

```bash
sudo docker exec clab-acl-srl sr_cli show system logging file acl_log
```
