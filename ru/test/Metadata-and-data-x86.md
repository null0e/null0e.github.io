```

Disassembly of section .init:

0000000000401000 <_init>:
  401000:       f3 0f 1e fa             endbr64
  401004:       48 83 ec 08             sub    $0x8,%rsp
  401008:       48 8b 05 e9 2f 00 00    mov    0x2fe9(%rip),%rax        # 403ff8 <__gmon_start__>
  40100f:       48 85 c0                test   %rax,%rax
  401012:       74 02                   je     401016 <_init+0x16>
  401014:       ff d0                   call   *%rax
  401016:       48 83 c4 08             add    $0x8,%rsp
  40101a:       c3                      ret

Disassembly of section .plt:

0000000000401020 <.plt>:
  401020:       ff 35 3a 2f 00 00       push   0x2f3a(%rip)        # 403f60 <_GLOBAL_OFFSET_TABLE_+0x8>
  401026:       f2 ff 25 3b 2f 00 00    bnd jmp *0x2f3b(%rip)        # 403f68 <_GLOBAL_OFFSET_TABLE_+0x10>
  40102d:       0f 1f 00                nopl   (%rax)
  401030:       f3 0f 1e fa             endbr64
  401034:       68 00 00 00 00          push   $0x0
  401039:       f2 e9 e1 ff ff ff       bnd jmp 401020 <.plt>
  40103f:       90                      nop
  401040:       f3 0f 1e fa             endbr64
  401044:       68 01 00 00 00          push   $0x1
  401049:       f2 e9 d1 ff ff ff       bnd jmp 401020 <.plt>
  40104f:       90                      nop
  401050:       f3 0f 1e fa             endbr64
  401054:       68 02 00 00 00          push   $0x2
  401059:       f2 e9 c1 ff ff ff       bnd jmp 401020 <.plt>
  40105f:       90                      nop
  401060:       f3 0f 1e fa             endbr64
  401064:       68 03 00 00 00          push   $0x3
  401069:       f2 e9 b1 ff ff ff       bnd jmp 401020 <.plt>
  40106f:       90                      nop
  401070:       f3 0f 1e fa             endbr64
  401074:       68 04 00 00 00          push   $0x4
  401079:       f2 e9 a1 ff ff ff       bnd jmp 401020 <.plt>
  40107f:       90                      nop
  401080:       f3 0f 1e fa             endbr64
  401084:       68 05 00 00 00          push   $0x5
  401089:       f2 e9 91 ff ff ff       bnd jmp 401020 <.plt>
  40108f:       90                      nop
  401090:       f3 0f 1e fa             endbr64
  401094:       68 06 00 00 00          push   $0x6
  401099:       f2 e9 81 ff ff ff       bnd jmp 401020 <.plt>
  40109f:       90                      nop
  4010a0:       f3 0f 1e fa             endbr64
  4010a4:       68 07 00 00 00          push   $0x7
  4010a9:       f2 e9 71 ff ff ff       bnd jmp 401020 <.plt>
  4010af:       90                      nop
  4010b0:       f3 0f 1e fa             endbr64
  4010b4:       68 08 00 00 00          push   $0x8
  4010b9:       f2 e9 61 ff ff ff       bnd jmp 401020 <.plt>
  4010bf:       90                      nop
  4010c0:       f3 0f 1e fa             endbr64
  4010c4:       68 09 00 00 00          push   $0x9
  4010c9:       f2 e9 51 ff ff ff       bnd jmp 401020 <.plt>
  4010cf:       90                      nop
  4010d0:       f3 0f 1e fa             endbr64
  4010d4:       68 0a 00 00 00          push   $0xa
  4010d9:       f2 e9 41 ff ff ff       bnd jmp 401020 <.plt>
  4010df:       90                      nop
  4010e0:       f3 0f 1e fa             endbr64
  4010e4:       68 0b 00 00 00          push   $0xb
  4010e9:       f2 e9 31 ff ff ff       bnd jmp 401020 <.plt>
  4010ef:       90                      nop
  4010f0:       f3 0f 1e fa             endbr64
  4010f4:       68 0c 00 00 00          push   $0xc
  4010f9:       f2 e9 21 ff ff ff       bnd jmp 401020 <.plt>
  4010ff:       90                      nop
  401100:       f3 0f 1e fa             endbr64
  401104:       68 0d 00 00 00          push   $0xd
  401109:       f2 e9 11 ff ff ff       bnd jmp 401020 <.plt>
  40110f:       90                      nop
  401110:       f3 0f 1e fa             endbr64
  401114:       68 0e 00 00 00          push   $0xe
  401119:       f2 e9 01 ff ff ff       bnd jmp 401020 <.plt>
  40111f:       90                      nop
  401120:       f3 0f 1e fa             endbr64
  401124:       68 0f 00 00 00          push   $0xf
  401129:       f2 e9 f1 fe ff ff       bnd jmp 401020 <.plt>
  40112f:       90                      nop

Disassembly of section .plt.sec:

0000000000401130 <__errno_location@plt>:
  401130:       f3 0f 1e fa             endbr64
  401134:       f2 ff 25 35 2e 00 00    bnd jmp *0x2e35(%rip)        # 403f70 <__errno_location@GLIBC_2.2.5>
  40113b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401140 <puts@plt>:
  401140:       f3 0f 1e fa             endbr64
  401144:       f2 ff 25 2d 2e 00 00    bnd jmp *0x2e2d(%rip)        # 403f78 <puts@GLIBC_2.2.5>
  40114b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401150 <write@plt>:
  401150:       f3 0f 1e fa             endbr64
  401154:       f2 ff 25 25 2e 00 00    bnd jmp *0x2e25(%rip)        # 403f80 <write@GLIBC_2.2.5>
  40115b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401160 <__stack_chk_fail@plt>:
  401160:       f3 0f 1e fa             endbr64
  401164:       f2 ff 25 1d 2e 00 00    bnd jmp *0x2e1d(%rip)        # 403f88 <__stack_chk_fail@GLIBC_2.4>
  40116b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401170 <dup2@plt>:
  401170:       f3 0f 1e fa             endbr64
  401174:       f2 ff 25 15 2e 00 00    bnd jmp *0x2e15(%rip)        # 403f90 <dup2@GLIBC_2.2.5>
  40117b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401180 <geteuid@plt>:
  401180:       f3 0f 1e fa             endbr64
  401184:       f2 ff 25 0d 2e 00 00    bnd jmp *0x2e0d(%rip)        # 403f98 <geteuid@GLIBC_2.2.5>
  40118b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401190 <fputc@plt>:
  401190:       f3 0f 1e fa             endbr64
  401194:       f2 ff 25 05 2e 00 00    bnd jmp *0x2e05(%rip)        # 403fa0 <fputc@GLIBC_2.2.5>
  40119b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004011a0 <read@plt>:
  4011a0:       f3 0f 1e fa             endbr64
  4011a4:       f2 ff 25 fd 2d 00 00    bnd jmp *0x2dfd(%rip)        # 403fa8 <read@GLIBC_2.2.5>
  4011ab:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004011b0 <strcmp@plt>:
  4011b0:       f3 0f 1e fa             endbr64
  4011b4:       f2 ff 25 f5 2d 00 00    bnd jmp *0x2df5(%rip)        # 403fb0 <strcmp@GLIBC_2.2.5>
  4011bb:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004011c0 <malloc@plt>:
  4011c0:       f3 0f 1e fa             endbr64
  4011c4:       f2 ff 25 ed 2d 00 00    bnd jmp *0x2ded(%rip)        # 403fb8 <malloc@GLIBC_2.2.5>
  4011cb:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004011d0 <__printf_chk@plt>:
  4011d0:       f3 0f 1e fa             endbr64
  4011d4:       f2 ff 25 e5 2d 00 00    bnd jmp *0x2de5(%rip)        # 403fc0 <__printf_chk@GLIBC_2.3.4>
  4011db:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004011e0 <setvbuf@plt>:
  4011e0:       f3 0f 1e fa             endbr64
  4011e4:       f2 ff 25 dd 2d 00 00    bnd jmp *0x2ddd(%rip)        # 403fc8 <setvbuf@GLIBC_2.2.5>
  4011eb:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004011f0 <open@plt>:
  4011f0:       f3 0f 1e fa             endbr64
  4011f4:       f2 ff 25 d5 2d 00 00    bnd jmp *0x2dd5(%rip)        # 403fd0 <open@GLIBC_2.2.5>
  4011fb:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401200 <exit@plt>:
  401200:       f3 0f 1e fa             endbr64
  401204:       f2 ff 25 cd 2d 00 00    bnd jmp *0x2dcd(%rip)        # 403fd8 <exit@GLIBC_2.2.5>
  40120b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401210 <__fprintf_chk@plt>:
  401210:       f3 0f 1e fa             endbr64
  401214:       f2 ff 25 c5 2d 00 00    bnd jmp *0x2dc5(%rip)        # 403fe0 <__fprintf_chk@GLIBC_2.3.4>
  40121b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

0000000000401220 <strerror@plt>:
  401220:       f3 0f 1e fa             endbr64
  401224:       f2 ff 25 bd 2d 00 00    bnd jmp *0x2dbd(%rip)        # 403fe8 <strerror@GLIBC_2.2.5>
  40122b:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

Disassembly of section .text:

0000000000401230 <disable_buffering>:
  401230:       f3 0f 1e fa             endbr64
  401234:       50                      push   %rax
  401235:       48 8b 3d f4 2d 00 00    mov    0x2df4(%rip),%rdi        # 404030 <stdin@GLIBC_2.2.5>
  40123c:       31 c9                   xor    %ecx,%ecx
  40123e:       ba 02 00 00 00          mov    $0x2,%edx
  401243:       31 f6                   xor    %esi,%esi
  401245:       e8 96 ff ff ff          call   4011e0 <setvbuf@plt>
  40124a:       48 8b 3d cf 2d 00 00    mov    0x2dcf(%rip),%rdi        # 404020 <stdout@GLIBC_2.2.5>
  401251:       b9 01 00 00 00          mov    $0x1,%ecx
  401256:       31 f6                   xor    %esi,%esi
  401258:       ba 02 00 00 00          mov    $0x2,%edx
  40125d:       41 58                   pop    %r8
  40125f:       e9 7c ff ff ff          jmp    4011e0 <setvbuf@plt>

0000000000401264 <main>:
  401264:       f3 0f 1e fa             endbr64
  401268:       55                      push   %rbp
  401269:       41 89 f8                mov    %edi,%r8d
  40126c:       b9 09 00 00 00          mov    $0x9,%ecx
  401271:       48 83 ec 20             sub    $0x20,%rsp
  401275:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
  40127c:       00 00 
  40127e:       48 89 44 24 18          mov    %rax,0x18(%rsp)
  401283:       31 c0                   xor    %eax,%eax
  401285:       48 8d 7c 24 0f          lea    0xf(%rsp),%rdi
  40128a:       41 ff c8                dec    %r8d
  40128d:       f3 aa                   rep stos %al,%es:(%rdi)
  40128f:       7e 4f                   jle    4012e0 <main+0x7c>
  401291:       48 8b 6e 08             mov    0x8(%rsi),%rbp
  401295:       48 83 c9 ff             or     $0xffffffffffffffff,%rcx
  401299:       48 8d 35 33 0e 00 00    lea    0xe33(%rip),%rsi        # 4020d3 <_IO_stdin_used+0xd3>
  4012a0:       48 89 ef                mov    %rbp,%rdi
  4012a3:       f2 ae                   repnz scas %es:(%rdi),%al
  4012a5:       48 f7 d1                not    %rcx
  4012a8:       48 8d 7c 0d fa          lea    -0x6(%rbp,%rcx,1),%rdi
  4012ad:       e8 fe fe ff ff          call   4011b0 <strcmp@plt>
  4012b2:       85 c0                   test   %eax,%eax
  4012b4:       74 15                   je     4012cb <main+0x67>
  4012b6:       48 8d 35 1c 0e 00 00    lea    0xe1c(%rip),%rsi        # 4020d9 <_IO_stdin_used+0xd9>
  4012bd:       bf 01 00 00 00          mov    $0x1,%edi
  4012c2:       31 c0                   xor    %eax,%eax
  4012c4:       e8 07 ff ff ff          call   4011d0 <__printf_chk@plt>
  4012c9:       eb 59                   jmp    401324 <main+0xc0>
  4012cb:       31 f6                   xor    %esi,%esi
  4012cd:       48 89 ef                mov    %rbp,%rdi
  4012d0:       31 c0                   xor    %eax,%eax
  4012d2:       e8 19 ff ff ff          call   4011f0 <open@plt>
  4012d7:       31 f6                   xor    %esi,%esi
  4012d9:       89 c7                   mov    %eax,%edi
  4012db:       e8 90 fe ff ff          call   401170 <dup2@plt>
  4012e0:       41 83 c8 ff             or     $0xffffffff,%r8d
  4012e4:       31 ff                   xor    %edi,%edi
  4012e6:       48 8d 74 24 0f          lea    0xf(%rsp),%rsi
  4012eb:       ba 09 00 00 00          mov    $0x9,%edx
  4012f0:       48 8d 0d 01 0e 00 00    lea    0xe01(%rip),%rcx        # 4020f8 <_IO_stdin_used+0xf8>
  4012f7:       e8 8f 02 00 00          call   40158b <read_exact>
  4012fc:       80 7c 24 0f 3c          cmpb   $0x3c,0xf(%rsp)
  401301:       75 15                   jne    401318 <main+0xb4>
  401303:       80 7c 24 10 49          cmpb   $0x49,0x10(%rsp)
  401308:       75 0e                   jne    401318 <main+0xb4>
  40130a:       80 7c 24 11 6d          cmpb   $0x6d,0x11(%rsp)
  40130f:       75 07                   jne    401318 <main+0xb4>
  401311:       80 7c 24 12 67          cmpb   $0x67,0x12(%rsp)
  401316:       74 14                   je     40132c <main+0xc8>
  401318:       48 8d 3d f7 0d 00 00    lea    0xdf7(%rip),%rdi        # 402116 <_IO_stdin_used+0x116>
  40131f:       e8 1c fe ff ff          call   401140 <puts@plt>
  401324:       83 cf ff                or     $0xffffffff,%edi
  401327:       e8 d4 fe ff ff          call   401200 <exit@plt>
  40132c:       80 7c 24 13 01          cmpb   $0x1,0x13(%rsp)
  401331:       48 8d 3d fb 0d 00 00    lea    0xdfb(%rip),%rdi        # 402133 <_IO_stdin_used+0x133>
  401338:       75 e5                   jne    40131f <main+0xbb>
  40133a:       66 83 7c 24 14 3b       cmpw   $0x3b,0x14(%rsp)
  401340:       48 8d 3d 08 0e 00 00    lea    0xe08(%rip),%rdi        # 40214f <_IO_stdin_used+0x14f>
  401347:       75 d6                   jne    40131f <main+0xbb>
  401349:       66 83 7c 24 16 11       cmpw   $0x11,0x16(%rsp)
  40134f:       48 8d 3d 11 0e 00 00    lea    0xe11(%rip),%rdi        # 402167 <_IO_stdin_used+0x167>
  401356:       75 c7                   jne    40131f <main+0xbb>
  401358:       bf eb 03 00 00          mov    $0x3eb,%edi
  40135d:       e8 5e fe ff ff          call   4011c0 <malloc@plt>
  401362:       48 8d 3d 17 0e 00 00    lea    0xe17(%rip),%rdi        # 402180 <_IO_stdin_used+0x180>
  401369:       48 89 c6                mov    %rax,%rsi
  40136c:       48 85 c0                test   %rax,%rax
  40136f:       74 ae                   je     40131f <main+0xbb>
  401371:       41 83 c8 ff             or     $0xffffffff,%r8d
  401375:       31 ff                   xor    %edi,%edi
  401377:       ba eb 03 00 00          mov    $0x3eb,%edx
  40137c:       48 8d 0d 32 0e 00 00    lea    0xe32(%rip),%rcx        # 4021b5 <_IO_stdin_used+0x1b5>
  401383:       e8 03 02 00 00          call   40158b <read_exact>
  401388:       31 c0                   xor    %eax,%eax
  40138a:       e8 07 01 00 00          call   401496 <win>
  40138f:       48 8b 44 24 18          mov    0x18(%rsp),%rax
  401394:       64 48 33 04 25 28 00    xor    %fs:0x28,%rax
  40139b:       00 00 
  40139d:       74 05                   je     4013a4 <main+0x140>
  40139f:       e8 bc fd ff ff          call   401160 <__stack_chk_fail@plt>
  4013a4:       48 83 c4 20             add    $0x20,%rsp
  4013a8:       31 c0                   xor    %eax,%eax
  4013aa:       5d                      pop    %rbp
  4013ab:       c3                      ret
  4013ac:       0f 1f 40 00             nopl   0x0(%rax)

00000000004013b0 <_start>:
  4013b0:       f3 0f 1e fa             endbr64
  4013b4:       31 ed                   xor    %ebp,%ebp
  4013b6:       49 89 d1                mov    %rdx,%r9
  4013b9:       5e                      pop    %rsi
  4013ba:       48 89 e2                mov    %rsp,%rdx
  4013bd:       48 83 e4 f0             and    $0xfffffffffffffff0,%rsp
  4013c1:       50                      push   %rax
  4013c2:       54                      push   %rsp
  4013c3:       49 c7 c0 50 16 40 00    mov    $0x401650,%r8
  4013ca:       48 c7 c1 e0 15 40 00    mov    $0x4015e0,%rcx
  4013d1:       48 c7 c7 64 12 40 00    mov    $0x401264,%rdi
  4013d8:       ff 15 12 2c 00 00       call   *0x2c12(%rip)        # 403ff0 <__libc_start_main@GLIBC_2.2.5>
  4013de:       f4                      hlt
  4013df:       90                      nop

00000000004013e0 <_dl_relocate_static_pie>:
  4013e0:       f3 0f 1e fa             endbr64
  4013e4:       c3                      ret
  4013e5:       66 2e 0f 1f 84 00 00    cs nopw 0x0(%rax,%rax,1)
  4013ec:       00 00 00 
  4013ef:       90                      nop

00000000004013f0 <deregister_tm_clones>:
  4013f0:       b8 10 40 40 00          mov    $0x404010,%eax
  4013f5:       48 3d 10 40 40 00       cmp    $0x404010,%rax
  4013fb:       74 13                   je     401410 <deregister_tm_clones+0x20>
  4013fd:       b8 00 00 00 00          mov    $0x0,%eax
  401402:       48 85 c0                test   %rax,%rax
  401405:       74 09                   je     401410 <deregister_tm_clones+0x20>
  401407:       bf 10 40 40 00          mov    $0x404010,%edi
  40140c:       ff e0                   jmp    *%rax
  40140e:       66 90                   xchg   %ax,%ax
  401410:       c3                      ret
  401411:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
  401418:       00 00 00 00 
  40141c:       0f 1f 40 00             nopl   0x0(%rax)

0000000000401420 <register_tm_clones>:
  401420:       be 10 40 40 00          mov    $0x404010,%esi
  401425:       48 81 ee 10 40 40 00    sub    $0x404010,%rsi
  40142c:       48 89 f0                mov    %rsi,%rax
  40142f:       48 c1 ee 3f             shr    $0x3f,%rsi
  401433:       48 c1 f8 03             sar    $0x3,%rax
  401437:       48 01 c6                add    %rax,%rsi
  40143a:       48 d1 fe                sar    $1,%rsi
  40143d:       74 11                   je     401450 <register_tm_clones+0x30>
  40143f:       b8 00 00 00 00          mov    $0x0,%eax
  401444:       48 85 c0                test   %rax,%rax
  401447:       74 07                   je     401450 <register_tm_clones+0x30>
  401449:       bf 10 40 40 00          mov    $0x404010,%edi
  40144e:       ff e0                   jmp    *%rax
  401450:       c3                      ret
  401451:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
  401458:       00 00 00 00 
  40145c:       0f 1f 40 00             nopl   0x0(%rax)

0000000000401460 <__do_global_dtors_aux>:
  401460:       f3 0f 1e fa             endbr64
  401464:       80 3d dd 2b 00 00 00    cmpb   $0x0,0x2bdd(%rip)        # 404048 <completed.8061>
  40146b:       75 13                   jne    401480 <__do_global_dtors_aux+0x20>
  40146d:       55                      push   %rbp
  40146e:       48 89 e5                mov    %rsp,%rbp
  401471:       e8 7a ff ff ff          call   4013f0 <deregister_tm_clones>
  401476:       c6 05 cb 2b 00 00 01    movb   $0x1,0x2bcb(%rip)        # 404048 <completed.8061>
  40147d:       5d                      pop    %rbp
  40147e:       c3                      ret
  40147f:       90                      nop
  401480:       c3                      ret
  401481:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
  401488:       00 00 00 00 
  40148c:       0f 1f 40 00             nopl   0x0(%rax)

0000000000401490 <frame_dummy>:
  401490:       f3 0f 1e fa             endbr64
  401494:       eb 8a                   jmp    401420 <register_tm_clones>

0000000000401496 <win>:
  401496:       f3 0f 1e fa             endbr64
  40149a:       55                      push   %rbp
  40149b:       31 f6                   xor    %esi,%esi
  40149d:       48 8d 3d 60 0b 00 00    lea    0xb60(%rip),%rdi        # 402004 <_IO_stdin_used+0x4>
  4014a4:       48 81 ec 10 01 00 00    sub    $0x110,%rsp
  4014ab:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
  4014b2:       00 00 
  4014b4:       48 89 84 24 08 01 00    mov    %rax,0x108(%rsp)
  4014bb:       00 
  4014bc:       31 c0                   xor    %eax,%eax
  4014be:       e8 2d fd ff ff          call   4011f0 <open@plt>
  4014c3:       85 c0                   test   %eax,%eax
  4014c5:       79 45                   jns    40150c <win+0x76>
  4014c7:       e8 64 fc ff ff          call   401130 <__errno_location@plt>
  4014cc:       8b 38                   mov    (%rax),%edi
  4014ce:       e8 4d fd ff ff          call   401220 <strerror@plt>
  4014d3:       48 8d 35 30 0b 00 00    lea    0xb30(%rip),%rsi        # 40200a <_IO_stdin_used+0xa>
  4014da:       bf 01 00 00 00          mov    $0x1,%edi
  4014df:       48 89 c2                mov    %rax,%rdx
  4014e2:       31 c0                   xor    %eax,%eax
  4014e4:       e8 e7 fc ff ff          call   4011d0 <__printf_chk@plt>
  4014e9:       e8 92 fc ff ff          call   401180 <geteuid@plt>
  4014ee:       85 c0                   test   %eax,%eax
  4014f0:       74 54                   je     401546 <win+0xb0>
  4014f2:       48 8d 3d 3b 0b 00 00    lea    0xb3b(%rip),%rdi        # 402034 <_IO_stdin_used+0x34>
  4014f9:       e8 42 fc ff ff          call   401140 <puts@plt>
  4014fe:       48 8d 3d 52 0b 00 00    lea    0xb52(%rip),%rdi        # 402057 <_IO_stdin_used+0x57>
  401505:       e8 36 fc ff ff          call   401140 <puts@plt>
  40150a:       eb 3a                   jmp    401546 <win+0xb0>
  40150c:       48 8d 6c 24 08          lea    0x8(%rsp),%rbp
  401511:       89 c7                   mov    %eax,%edi
  401513:       ba 00 01 00 00          mov    $0x100,%edx
  401518:       48 89 ee                mov    %rbp,%rsi
  40151b:       e8 80 fc ff ff          call   4011a0 <read@plt>
  401520:       85 c0                   test   %eax,%eax
  401522:       7f 2a                   jg     40154e <win+0xb8>
  401524:       e8 07 fc ff ff          call   401130 <__errno_location@plt>
  401529:       8b 38                   mov    (%rax),%edi
  40152b:       e8 f0 fc ff ff          call   401220 <strerror@plt>
  401530:       48 8d 35 72 0b 00 00    lea    0xb72(%rip),%rsi        # 4020a9 <_IO_stdin_used+0xa9>
  401537:       bf 01 00 00 00          mov    $0x1,%edi
  40153c:       48 89 c2                mov    %rax,%rdx
  40153f:       31 c0                   xor    %eax,%eax
  401541:       e8 8a fc ff ff          call   4011d0 <__printf_chk@plt>
  401546:       83 cf ff                or     $0xffffffff,%edi
  401549:       e8 b2 fc ff ff          call   401200 <exit@plt>
  40154e:       48 63 d0                movslq %eax,%rdx
  401551:       48 89 ee                mov    %rbp,%rsi
  401554:       bf 01 00 00 00          mov    $0x1,%edi
  401559:       e8 f2 fb ff ff          call   401150 <write@plt>
  40155e:       48 8d 3d 6c 0b 00 00    lea    0xb6c(%rip),%rdi        # 4020d1 <_IO_stdin_used+0xd1>
  401565:       e8 d6 fb ff ff          call   401140 <puts@plt>
  40156a:       48 8b 84 24 08 01 00    mov    0x108(%rsp),%rax
  401571:       00 
  401572:       64 48 33 04 25 28 00    xor    %fs:0x28,%rax
  401579:       00 00 
  40157b:       74 05                   je     401582 <win+0xec>
  40157d:       e8 de fb ff ff          call   401160 <__stack_chk_fail@plt>
  401582:       48 81 c4 10 01 00 00    add    $0x110,%rsp
  401589:       5d                      pop    %rbp
  40158a:       c3                      ret

000000000040158b <read_exact>:
  40158b:       f3 0f 1e fa             endbr64
  40158f:       41 54                   push   %r12
  401591:       48 63 d2                movslq %edx,%rdx
  401594:       49 89 cc                mov    %rcx,%r12
  401597:       55                      push   %rbp
  401598:       44 89 c5                mov    %r8d,%ebp
  40159b:       53                      push   %rbx
  40159c:       48 89 d3                mov    %rdx,%rbx
  40159f:       e8 fc fb ff ff          call   4011a0 <read@plt>
  4015a4:       39 c3                   cmp    %eax,%ebx
  4015a6:       74 2e                   je     4015d6 <read_exact+0x4b>
  4015a8:       48 8b 3d 91 2a 00 00    mov    0x2a91(%rip),%rdi        # 404040 <stderr@GLIBC_2.2.5>
  4015af:       4c 89 e2                mov    %r12,%rdx
  4015b2:       be 01 00 00 00          mov    $0x1,%esi
  4015b7:       31 c0                   xor    %eax,%eax
  4015b9:       e8 52 fc ff ff          call   401210 <__fprintf_chk@plt>
  4015be:       48 8b 35 7b 2a 00 00    mov    0x2a7b(%rip),%rsi        # 404040 <stderr@GLIBC_2.2.5>
  4015c5:       bf 0a 00 00 00          mov    $0xa,%edi
  4015ca:       e8 c1 fb ff ff          call   401190 <fputc@plt>
  4015cf:       89 ef                   mov    %ebp,%edi
  4015d1:       e8 2a fc ff ff          call   401200 <exit@plt>
  4015d6:       5b                      pop    %rbx
  4015d7:       5d                      pop    %rbp
  4015d8:       41 5c                   pop    %r12
  4015da:       c3                      ret
  4015db:       0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)

00000000004015e0 <__libc_csu_init>:
  4015e0:       f3 0f 1e fa             endbr64
  4015e4:       41 57                   push   %r15
  4015e6:       4c 8d 3d 63 27 00 00    lea    0x2763(%rip),%r15        # 403d50 <__frame_dummy_init_array_entry>
  4015ed:       41 56                   push   %r14
  4015ef:       49 89 d6                mov    %rdx,%r14
  4015f2:       41 55                   push   %r13
  4015f4:       49 89 f5                mov    %rsi,%r13
  4015f7:       41 54                   push   %r12
  4015f9:       41 89 fc                mov    %edi,%r12d
  4015fc:       55                      push   %rbp
  4015fd:       48 8d 2d 5c 27 00 00    lea    0x275c(%rip),%rbp        # 403d60 <__do_global_dtors_aux_fini_array_entry>
  401604:       53                      push   %rbx
  401605:       4c 29 fd                sub    %r15,%rbp
  401608:       48 83 ec 08             sub    $0x8,%rsp
  40160c:       e8 ef f9 ff ff          call   401000 <_init>
  401611:       48 c1 fd 03             sar    $0x3,%rbp
  401615:       74 1f                   je     401636 <__libc_csu_init+0x56>
  401617:       31 db                   xor    %ebx,%ebx
  401619:       0f 1f 80 00 00 00 00    nopl   0x0(%rax)
  401620:       4c 89 f2                mov    %r14,%rdx
  401623:       4c 89 ee                mov    %r13,%rsi
  401626:       44 89 e7                mov    %r12d,%edi
  401629:       41 ff 14 df             call   *(%r15,%rbx,8)
  40162d:       48 83 c3 01             add    $0x1,%rbx
  401631:       48 39 dd                cmp    %rbx,%rbp
  401634:       75 ea                   jne    401620 <__libc_csu_init+0x40>
  401636:       48 83 c4 08             add    $0x8,%rsp
  40163a:       5b                      pop    %rbx
  40163b:       5d                      pop    %rbp
  40163c:       41 5c                   pop    %r12
  40163e:       41 5d                   pop    %r13
  401640:       41 5e                   pop    %r14
  401642:       41 5f                   pop    %r15
  401644:       c3                      ret
  401645:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
  40164c:       00 00 00 00 

0000000000401650 <__libc_csu_fini>:
  401650:       f3 0f 1e fa             endbr64
  401654:       c3                      ret

Disassembly of section .fini:

0000000000401658 <_fini>:
  401658:       f3 0f 1e fa             endbr64
  40165c:       48 83 ec 08             sub    $0x8,%rsp
  401660:       48 83 c4 08             add    $0x8,%rsp
  401664:       c3                      ret

```

Ниже — точные адреса и инструкции, которые определяют формат входа.

Code

```
401291: mov    0x8(%rsi),%rbp        ; argv[1]
401295: or     $-1,%rcx
401299: lea    0xe33(%rip),%rsi      ; ".cimg"
4012a3: repnz scasb
4012a8: lea    -0x6(%rbp,%rcx,1),%rdi ; argv[1] + len - 5
4012ad: call   strcmp
4012b2: test   %eax,%eax
4012b4: je     4012cb
```

Это сравнение `strcmp(argv[1] + strlen(argv[1]) - 5, ".cimg")`.


Code

```
4012e6: lea    0xf(%rsp),%rsi
4012eb: mov    $0x9,%edx
4012f7: call   read_exact
```

То есть бинарник ждёт **ровно 9 байт**.

Code

```
4012fc: cmpb $0x3c,0xf(%rsp)   ; '<'
401303: cmpb $0x49,0x10(%rsp)  ; 'I'
40130a: cmpb $0x6d,0x11(%rsp)  ; 'm'
401311: cmpb $0x67,0x12(%rsp)  ; 'g'
```

Это первые 4 байта: `3C 49 6D 67` → `<Img`

Проверка следующих 5 байт

Code

```
40132c: cmpb $0x1,0x13(%rsp)         ; version?
40133a: cmpw $0x3b,0x14(%rsp)        ; width = 0x003B
401349: cmpw $0x11,0x16(%rsp)        ; height = 0x0011
```

Итого:

Code

```
offset 4: 01
offset 5–6: 3B 00
offset 7–8: 11 00
```

Выделение буфера и чтение оставшихся данных

Code

```
401358: mov $0x3eb,%edi        ; malloc(0x3EB)
40137b: mov $0x3eb,%edx        ; read_exact(..., 0x3EB)
```

То есть бинарник ждёт **ещё 1003 байта**.

Вызов win()

Code

```
40138a: call win
```

script.py
```
#!/usr/bin/env python3
import struct

prefix = b"\x3C\x49\x6D\x67"      # "<Img"
prefix += b"\x01"                 # version
prefix += struct.pack("<H", 0x3B) # width
prefix += struct.pack("<H", 0x11) # height

payload = b"A" * 0x3EB            # 1003 bytes

with open("solution.cimg", "wb") as f:
    f.write(prefix + payload)
```