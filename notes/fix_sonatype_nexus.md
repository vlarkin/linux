
## Some commands for maintaining Sonatype Nexus

### Relocating a Blob Store

Shut down the repository manager and backup the data directory.  
Move the specified blob store directory to its new location.

```console
# move /storage/nexus/blobs/docker /nexus-data/blobs/
```

Run the OrientDB console
```console
# java -jar /opt/sonatype/nexus/lib/support/nexus-orient-console.jar
```

Connect to the config db
```text
orientdb> connect plocal:/opt/sonatype/sonatype-work/nexus3/db/config admin admin
```

Change settings and exit from the console
```text
orientdb {db=config}> update repository_blobstore set attributes.file.path='/nexus-data/blobs/docker' where name='docker'
orientdb {db=config}> disconnect
orientdb> exit
```

Start up the repository manager.

### Fix a corrupted OrientDB after unclean shutdown

Run the OrientDB console.  
Connect to the database and run rebuild and repair commands
```text
orientdb> CONNECT PLOCAL:/opt/sonatype/sonatype-work/nexus3/db/config admin admin
orientdb {db=config}> REBUILD INDEX *
orientdb {db=config}> REPAIR DATABASE --fix-graph
orientdb {db=config}> REPAIR DATABASE --fix-links
orientdb {db=config}> REPAIR DATABASE --fix-ridbags
orientdb {db=config}> REPAIR DATABASE --fix-bonsai
orientdb {db=config}> DISCONNECT
```
