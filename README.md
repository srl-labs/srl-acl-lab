# Access Control Lists on SR Linux

[![Discord][discord-svg]][discord-url] [![DevPod][devpod-svg]][devpod-url] [![Codespaces][codespaces-svg]][codespaces-url]  
![w212][w212][Learn more](https://devpod.sh)![w90][w90][Learn more](https://containerlab.dev/manual/codespaces)

Get to know ACLs on SR Linux!

After lab is started the following ping should succeed, as there is no default ACL in place.

```
sudo docker exec -i -t acl-client ping -w 2 -c 2 192.168.20.100
```

Then configure the ACL on ethernet-1/1.0 subinterface of SR Linux to drop ICMP packets destined towards the server:

```bash
cat icmp_drop.cfg | docker exec -i acl-srl sr_cli -e -c
```

Repeat the ping, it should not succeed, as the ICMP drop ACL is in place. You can check the logs on SR Linux to ensure that the packets are being dropped:

```bash
sudo docker exec acl-srl sr_cli show system logging file acl_log
```

[discord-svg]: https://gitlab.com/rdodin/pics/-/wikis/uploads/b822984bc95d77ba92d50109c66c7afe/join-discord-btn.svg
[discord-url]: https://discord.gg/tZvgjQ6PZf
[devpod-svg]: https://gitlab.com/rdodin/pics/-/wikis/uploads/dfc36636ecaa60f3e70340686d5800db/open-in-devpod-btn.svg
[devpod-url]: https://devpod.sh/open#https://github.com/srl-labs/srl-acl-lab
[codespaces-svg]: https://gitlab.com/rdodin/pics/-/wikis/uploads/80546a8c7cda8bb14aa799d26f55bd83/run-codespaces-btn.svg
[codespaces-url]: https://codespaces.new/srl-labs/srl-acl-lab?quickstart=1&devcontainer_path=.devcontainer%2Fdocker-in-docker%2Fdevcontainer.json
[w212]: https://gitlab.com/rdodin/pics/-/wikis/uploads/718a32dfa2b375cb07bcac50ae32964a/w212h1.svg
[w90]: https://gitlab.com/rdodin/pics/-/wikis/uploads/bf1b8ea28b4528eb1b66567355a13c5c/w90h1.svg
