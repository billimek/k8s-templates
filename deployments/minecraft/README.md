# Minecraft

![](https://i.imgur.com/zBha0RP.png)

## installing

```shell
helm install --name mc stable/minecraft --values values.yaml --set minecraftServer.gameMode="creative",minecraftServer.ops="83d9416e-216e-4ffb-81ae-d2bd455a398a",minecraftServer.motd="billimek minecraft server (creative)"
helm install --name mcsv stable/minecraft --values values.yaml --set minecraftServer.gameMode="survival",minecraftServer.ops="83d9416e-216e-4ffb-81ae-d2bd455a398a",minecraftServer.motd="billimek minecraft server (survival)"


```

## upgrading
```shell
helm upgrade mc stable/minecraft --reset-values --values values.yaml --set minecraftServer.gameMode="creative",minecraftServer.ops="83d9416e-216e-4ffb-81ae-d2bd455a398a",minecraftServer.motd="billimek minecraft server (creative)"
helm upgrade mcsv stable/minecraft --reset-values --values values.yaml --set minecraftServer.gameMode="survival",minecraftServer.ops="83d9416e-216e-4ffb-81ae-d2bd455a398a",minecraftServer.motd="billimek minecraft server (survival)"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
