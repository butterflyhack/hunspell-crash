# hunspell-crash
find a crash by libfuzzer , the crash was caused by a invalid READ memory access.

$cd crash
#
$./first_fuzzer crash-*

```
==70237==ERROR: AddressSanitizer: SEGV on unknown address 0xfffffffffffffffe (pc 0x000000548e7c bp 0x7ffc24a458e0 sp 0x7ffc24a458b0 T0)
==70237==The signal is caused by a READ memory access.
    #0 0x548e7b in std::vector<w_char, std::allocator<w_char> >::operator[](unsigned long) const /usr/bin/../lib/gcc/x86_64-linux-gnu/5.4.0/../../../../include/c++/5.4.0/bits/stl_vector.h:795:41
    #1 0x548e7b in SuggestMgr::leftcommonsubstring(std::vector<w_char, std::allocator<w_char> > const&, std::vector<w_char, std::allocator<w_char> > const&) /home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/src/hunspell/./suggestmgr.cxx:2043
    #2 0x5448be in SuggestMgr::ngsuggest(std::vector<std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >, std::allocator<std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > > >&, char const*, std::vector<HashMgr*, std::allocator<HashMgr*> > const&, int) /home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/src/hunspell/./suggestmgr.cxx:1194:26
    #3 0x5353f1 in HunspellImpl::suggest_internal(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, bool&, unsigned long&, int&) /home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/src/hunspell/./hunspell.cxx:1194:16
    #4 0x5339ee in HunspellImpl::suggest(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&) /home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/src/hunspell/./hunspell.cxx:899:35
    #5 0x53bf10 in Hunspell::suggest(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&) /home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/src/hunspell/./hunspell.cxx:2042:18
    #6 0x52b80b in LLVMFuzzerTestOneInput /home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/tests/fuzzer1.cxx:82:19
    #7 0x42fe2a in fuzzer::Fuzzer::ExecuteCallback(unsigned char const*, unsigned long) (/home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/tests/crash_test+0x42fe2a)
    #8 0x41ffae in fuzzer::RunOneTest(fuzzer::Fuzzer*, char const*, unsigned long) (/home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/tests/crash_test+0x41ffae)
    #9 0x4258a1 in fuzzer::FuzzerDriver(int*, char***, int (*)(unsigned char const*, unsigned long)) (/home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/tests/crash_test+0x4258a1)
    #10 0x44e372 in main (/home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/tests/crash_test+0x44e372)
    #11 0x7fe57050582f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291
    #12 0x41e8a8 in _start (/home/butterfly/Desktop/hunspell-1.7.0/hunspell-1.7.0/tests/crash_test+0x41e8a8)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV /usr/bin/../lib/gcc/x86_64-linux-gnu/5.4.0/../../../../include/c++/5.4.0/bits/stl_vector.h:795:41 in std::vector<w_char, std::allocator<w_char> >::operator[](unsigned long) const
==70237==ABORTING
```

