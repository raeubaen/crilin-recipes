# openstack-tunnel

Questa repo contiene solo una lista di istruzioni per accedere da una qualsiasi macchina A (nome utente: userA), normalmente non accessibile dall'esterno, ad una qualsiasi macchina B (nome utente: userB), normalmente non accessibile dall'esterno, passando per la macchina C, che è la mia VM di openstack (root@ruben-openstack.cern.ch).

Vanno inserite sulle macchine A e B queste righe:
```
ServerAliveInterval 5

Host lxtunnel
  HostName lxtunnel.cern.ch
  User rgargiul
  AddressFamily inet

Host ruben-openstack
  User root
  HostName ruben-openstack.cern.ch
  ProxyJump lxtunnel

GSSAPIAuthentication yes
GSSAPIDelegateCredentials yes

```

Vanno anche copiati i file ~/.ssh/id_rsa e ~/.ssh/id_rsa.pub dal mio lxplus alle macchine A e B, per fare credere a openstack che ci stiamo collegando da lxplus.
Vanno cambiati i permessi al file ~/.ssh/id_rsa con chmod 600.

Sulla macchina B (quella a cui ci vogliamo collegare), va aperta una shell (che va lasciata sempre accesa, magari con screen), e va eseguito:
```
ssh -N -R 2222:localhost:22 root@ruben-openstack
```

Sulla macchina A, per collegarsi alla macchine B, va eseguito:
```
ssh -J root@ruben-openstack -p 2222 userB@localhost
```

Forse nel dubbio è meglio accendere un servizio autossh sulla macchina B, oltre a un team Viewer per gestire eventuali problemi
