# collabora_traefik
simple docker container using traefik to setup a collabora server, optionally with config file


This repository sets up a collabora server at the given domain.
To start the server:
 1. clone this repository locally
 2. cd into the toplevel directory
 3. edit the .env file. You need to at least set the url to get the compose to run
 4. run docker compose up -d (or docker-compose up -d depending on docker version)

the coolwsd file can be used to change config values, for example you can set a regex filter which servers can use the collabora server:
```
   <storage desc="Backend storage">
        <filesystem allow="false" />
        <wopi desc="Allow/deny wopi storage." allow="true">
            <max_file_size desc="Maximum document size in bytes to load. 0 for unlimited." type="uint">0</max_file_size>
            <locking desc="Locking settings">
                <refresh desc="How frequently we should re-acquire a lock with the storage server, in seconds (default 15 mins) or 0 for no refresh" type="int" default="900">900</refresh>
            </locking>

            <alias_groups desc="default mode is 'first' it allows only the first host when groups are not defined. set mode to 'groups' and define group to allow multiple host and its aliases" mode="groups">
            <!-- If you need to use multiple wopi hosts, please change the mode to "groups" and
                    add the hosts below.  If one host is accessible under multiple ip addresses
                    or names, add them as aliases. -->
            <group>
                    <host desc="hostname to allow or deny." allow="true">https://example.url</host>
		    <alias desc="regex pattern of aliasname">https://.*first.*url.*</alias>	    
            </group>		
            <group>
		    <host desc="hostname to allow or deny." allow="true">https://example2.url</host>
		    <alias desc="regex pattern of aliasname">https://.*secondurl.*</alias>	    
            </group>		    		    
            <!-- More "group"s possible here -->
            </alias_groups>
```
