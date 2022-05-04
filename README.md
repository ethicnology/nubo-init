# nobu-init

## multipass
[Multipass](https://multipass.run/) is a lightweight VM manager for **Linux, Windows and macOS**. It's designed for developers who want a fresh Ubuntu environment with a single command. It uses KVM on Linux, Hyper-V on Windows and HyperKit on macOS to run the VM with minimal overhead. It can also use VirtualBox on Windows and macOS. Multipass will fetch images for you and keep them up to date.

Since it supports metadata for cloud-init, you can simulate a small cloud deployment on your laptop or workstation.

### QEMU -> LXD
```sh
multipass set local.driver=lxd
```

## usage
### jellyfin
```sh
multipass launch 20.04 --name jellyfin --cloud-init jellyfin.yaml
```

```sh
multipass exec jellyfin -- sudo service jellyfin status
# ● jellyfin.service - Jellyfin Media Server
#      Loaded: loaded (/lib/systemd/system/jellyfin.service; enabled; vendor pres>
#     Drop-In: /etc/systemd/system/jellyfin.service.d
#              └─jellyfin.service.conf
#      Active: active (running) since Wed 2022-05-04 11:55:38 CEST; 1min 37s ago
```

### bitcoin
```sh
multipass launch --name btc --cloud-init jellyfin.yaml --disk 40G # testnet blockchain
```

```sh
multipass exec btc -- bitcoin-cli -testnet getblockchaininfo
# {
#   "chain": "test",
#   "blocks": 0,
#   "headers": 0,
#   "bestblockhash": "000000000933ea01ad0ee984209779baaec3ced90fa3f408719526f8d77f4943",
#   "difficulty": 1,
#   "time": 1296688602,
#   "mediantime": 1296688602,
#   "verificationprogress": 1.595119552376496e-08,
#   "initialblockdownload": true,
#   "chainwork": "0000000000000000000000000000000000000000000000000000000100010001",
#   "size_on_disk": 293,
#   "pruned": false,
#   "warnings": ""
# }
```