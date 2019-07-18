# mafiapp demonstrating mnesia #

Based on [Learn You Some Erlang](http://learnyousomeerlang.com/mnesia)

## Running ##
rebar3 compile
werl -pa _build/default/lib/*/ebin/ -sname test

### memory test
mnesia:delete_schema([node()]).
application:start(recon).
mafiapp:install([node()]).
application:ensure_all_started(mafiapp).
recon_alloc:set_unit(megabyte).
recon_alloc:memory(unused). 
recon_alloc:memory(used).
[mafiapp:add_friend("Don Corleone" ++ integer_to_list(N), [], [boss], boss) || N <- lists:seq(1, 1000000)].
recon_alloc:memory(unused). 
recon_alloc:memory(used).
mnesia:delete_table(mafiapp_friends).
recon_alloc:memory(unused). 
recon_alloc:memory(used).
