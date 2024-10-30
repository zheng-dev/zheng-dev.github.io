erl反编译
---------
没加debug_info的也能看`erlang:display(beam_disasm:file("fight_test_port.beam")).`,
可以直接编译出汇编指令`erlc +S your_module.erl`

erl安装
-------
```bash
tar -zxf otp_src_24.3.4.12.tar.gz
cd 源码包
./configure  --prefix=/usr/local/erlang24
make && make install
```

```erlang
erl_boot_server:add_slave({172,16,0,1}),
erl_boot_server:which_slaves().
%
{ok, Socket} = gen_udp:open(0, [binary]).   
{ok,#Port<0.4>}
gen_udp:send(Socket, "192.168.22.9", 2881, 3).      
```

```bash
[root@xxx ss]# ps -axuw |less
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
game_se+     669  0.0  0.0  12140   104 ?        S    13:20   0:00 /data/ss/t/slave/erlang/erts-12.3.2.12/bin/epmd -daemon
game_se+   23686  0.1  0.3 3400924 120476 ?      Sl   13:29   0:00 /data/ss/t/slave/erlang/erts-12.3.2.12/bin/beam.smp -- -root /data/ss/boot/erlang -progname erl -- -home /data/ss/t/slave/erlang -- /data/ss/t/slave/erlang /data/ss/boot/erlang -noshell -noinput -boot start_sasl -config slave -setcookie test1 -loader inet -hosts 172.16.0.10 -name x@172.16.0.11 -id x@172.16.0.11 -s net_adm ping_list m1@172.16.0.10 -s main slave_start -kernel inet_dist_listen_min 40501 inet_dist_listen_max 40501
game_se+   23691  0.0  0.0   4388   932 ?        Ss   13:29   0:00 erl_child_setup 4000000
game_se+   23760  0.0  0.0  12132  1252 ?        Ss   13:29   0:00 inet_gethost 4
```