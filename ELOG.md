# per accedere da mu2edaq
- aprire il browser
- andare su localhost:8080

# per accedere da remoto:
dentro la VPN di Frascati sul proprio computer locale:

ssh -L 8080:localhost:8080 mu2e@mu2edaq

nel browser del proprio computer locale:
localhost:8080
a questo punto si vedono gli ELOG


# (temporaneo, potrebbe non funzionare) per accedere da remoto senza ssh e VPN:
http://crilinelog.nglocalhost.com/demo/

Cosa c'è sotto:
Dato che aprire un tunnel verso l'esterno (il server nglocalhost.com, di cui non sappiamo nulla) da LNF direttamente non mi sembrava opportuno, lo facciamo passando per il CERN

Si seguono le istruzioni qui https://github.com/raeubaen/crilin-recipes/blob/main/openstack-tunnel-CERN.md
e poi dentro screen si accende:
ssh -N -R 8080:localhost:8080 root@ruben-openstack

in uno screen su root@ruben-openstack si accende:
ssh -R crilinelog.nglocalhost.com:80:localhost:8080 nglocalhost.com
