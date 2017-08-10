## Tools to copy Neo4j Stores between versions

Uses the batch-inserter API to read and write the stores keeping the node-ids.
Copies the manual index-files as is.
Ignores broken nodes and relationships.

Also useful to skip no longer wanted properties or relationships with a certain type. Good for store compaction as it
rewrites the store file reclaiming space that is sitting empty.

It uses local .m2 repositories of the Neo4j versions that you provide.

### Store Copy

Usage:

    # build all the shadow-jars
    mvn clean install
    
    cd runner
    mvn compile exec:java -Dexec.mainClass="org.neo4j.tool.StoreCopyRevert" \
      -Dexec.args="/path/to/source:version /path/to/target:version [rel,types,to,ignore] [properties,to,ignore]"

e.g. 

    mvn compile exec:java -Dexec.mainClass="org.neo4j.tool.StoreCopyRevert" \
      -Dexec.args="/backup/test.db:3.2 /tmp/fixed.db:3.1 :FOO bar"

Supported versions

* 3.1.5
* 3.2.3
* 3.0.11
* 2.3.11
* 2.2.10
