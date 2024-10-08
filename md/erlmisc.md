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