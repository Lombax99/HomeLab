[link installazione ufficiale](https://foundryvtt.com/article/installation/)
[minimum requirements](https://foundryvtt.com/article/requirements/)
[foundry wiki](https://foundryvtt.wiki/en/setup)

[foundry swag docker](https://github.com/ChefsSlaad/foundry_swag_docker/tree/main)
Ho seguito quest'ultimo tutorial con un paio di note:
1) il docker di foundry usato nel tutorial non è più disponibile quindi ne ho dovuto usare un altro, ho preso quello banalotto dalla wiki di foundry
2) nginx vuole che tutti i file di conf per fare da reverse proxy finiscano con .conf
3) nel file di conf del reverse proxy la definizione del link a cui forwardare mi manda in redirect loop, per evitare il problema ho definito io a mano il link come http://foundry:3000/ 
4) Serve fare portforwarding anche della porta 80 come indicato nel tutorial per check di nginx


Da fare ogni tanto:
```bash
sudo apt update
sudo apt upgrade
```


### Updating Foundry
La maggior parte degli update possono essere fatti direttamente da foundry ma in alcuni casi, in corrispondenza di patch maggiori l'app potrebbe richiedere di essere aggiornata manualmente:

