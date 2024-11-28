Il tuo script `sh` ha un paio di problemi che devono essere corretti. 

1. Il comando `ping` necessita di un indirizzo IP o un hostname valido per funzionare. `0.0` non è un indirizzo valido.
2. La sintassi della struttura `while` è corretta, ma è meglio utilizzare un `sleep` per evitare che il ciclo venga eseguito in modo continuo, ad esempio ogni secondo.

Ecco un esempio corretto di come potrebbe apparire il tuo script `sh` per pingare un indirizzo IP (ad esempio, `8.8.8.8`, che è uno dei server DNS pubblici di Google) in un ciclo infinito, con una pausa di un secondo tra i ping:

```sh
#!/bin/sh

while true; do
    ping -c 1 8.8.8.8  # Pinga un pacchetto
    sleep 1           # Aspetta 1 secondo prima del prossimo ping
done
```

### Spiegazione:
- `#!/bin/sh`: specifica quale interprete utilizzare per eseguire il file.
- `ping -c 1 8.8.8.8`: esegue un ping all'indirizzo IP specificato e fa un solo ping (`-c 1`).
- `sleep 1`: introduce una pausa di 1 secondo tra ogni ping.

Assicurati di avere i permessi di esecuzione sul file. Puoi farlo con il comando:

```sh
chmod +x nome_del_file.sh
```

E poi puoi eseguire il tuo script con:

```sh
./nome_del_file.sh
``` 

Sostituisci `nome_del_file.sh` con il nome effettivo del tuo file.