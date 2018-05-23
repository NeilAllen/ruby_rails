The error is something akin to this.

```Building native extensions.  This could take a while...
ERROR:  Error installing ovirt-engine-sdk:
  ERROR: Failed to build gem native extension.

    current directory: /Users/cricket/.rvm/gems/ruby-2.4.3@afar/gems/ovirt-engine-sdk-4.2.4/ext/ovirtsdk4c
/Users/cricket/.rvm/rubies/ruby-2.4.3/bin/ruby -r ./siteconf20180522-37367-1g6s58w.rb extconf.rb
checking for xml2-config... yes
checking for curl-config... yes
creating Makefile

current directory: /Users/cricket/.rvm/gems/ruby-2.4.3@afar/gems/ovirt-engine-sdk-4.2.4/ext/ovirtsdk4c
make "DESTDIR=" clean

current directory: /Users/cricket/.rvm/gems/ruby-2.4.3@afar/gems/ovirt-engine-sdk-4.2.4/ext/ovirtsdk4c
make "DESTDIR="
compiling ov_error.c
compiling ov_http_client.c
ov_http_client.c:392:33: warning: comparison of integers of different signs: 'long' and 'size_t' (aka 'unsigned long') [-Wsign-compare]
        while (pointer - buffer < length && isspace(*pointer)) {
               ~~~~~~~~~~~~~~~~ ^ ~~~~~~
ov_http_client.c:651:18: warning: implicit conversion loses integer precision: 'long' to 'int' [-Wshorten-64-to-32]
    ptr->limit = connections;
               ~ ^~~~~~~~~~~
ov_http_client.c:845:71: warning: implicit conversion loses integer precision: 'long' to 'int' [-Wshorten-64-to-32]
    context_ptr->code = curl_multi_wait(context_ptr->handle, NULL, 0, timeout, NULL);
                        ~~~~~~~~~~~~~~~                               ^~~~~~~
ov_http_client.c:1092:34: warning: comparison of integers of different signs: 'unsigned long' and 'int' [-Wsign-compare]
    if (RHASH_SIZE(ptr->pending) < ptr->limit) {
        ~~~~~~~~~~~~~~~~~~~~~~~~ ^ ~~~~~~~~~~
ov_http_client.c:1118:71: warning: comparison of integers of different signs: 'unsigned long' and 'int' [-Wsign-compare]
        while (RARRAY_LEN(ptr->queue) > 0 && RHASH_SIZE(ptr->pending) < ptr->limit) {
                                             ~~~~~~~~~~~~~~~~~~~~~~~~ ^ ~~~~~~~~~~
5 warnings generated.
compiling ov_http_request.c
compiling ov_http_response.c
compiling ov_http_transfer.c
compiling ov_module.c
compiling ov_string.c
compiling ov_xml_reader.c
ov_xml_reader.c:109:14: warning: implicit conversion loses integer precision: 'long' to 'int' [-Wshorten-64-to-32]
    length = RSTRING_LEN(data);
           ~ ^~~~~~~~~~~~~~~~~
/Users/cricket/.rvm/rubies/ruby-2.4.3/include/ruby-2.4.0/ruby/ruby.h:980:6: note: expanded from macro 'RSTRING_LEN'
     RSTRING_EMBED_LEN(str) : \
     ^~~~~~~~~~~~~~~~~~~~~~
/Users/cricket/.rvm/rubies/ruby-2.4.3/include/ruby-2.4.0/ruby/ruby.h:976:6: note: expanded from macro 'RSTRING_EMBED_LEN'
     (long)((RBASIC(str)->flags >> RSTRING_EMBED_LEN_SHIFT) & \
     ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ov_xml_reader.c:109:14: warning: implicit conversion loses integer precision: 'long' to 'int' [-Wshorten-64-to-32]
    length = RSTRING_LEN(data);
           ~ ^~~~~~~~~~~~~~~~~
/Users/cricket/.rvm/rubies/ruby-2.4.3/include/ruby-2.4.0/ruby/ruby.h:981:28: note: expanded from macro 'RSTRING_LEN'
     RSTRING(str)->as.heap.len)
     ~~~~~~~~~~~~~~~~~~~~~~^~~
2 warnings generated.
compiling ov_xml_writer.c
compiling ovirtsdk4c.c
linking shared-object ovirtsdk4c.bundle
ld: file not found: /usr/lib/system/libsystem_darwin.dylib for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make: *** [ovirtsdk4c.bundle] Error 1

make failed, exit code 2

Gem files will remain installed in /Users/cricket/.rvm/gems/ruby-2.4.3@afar/gems/ovirt-engine-sdk-4.2.4 for inspection.
Results logged to /Users/cricket/.rvm/gems/ruby-2.4.3@afar/extensions/x86_64-darwin-16/2.4.0/ovirt-engine-sdk-4.2.4/gem_make.out
```


I did **2 things** and I'm not sure which one "fixed" it.
1. update Xcode to 9.2 or greater. Check your version: `/usr/bin/xcodebuild -version`
2. based on [this help page](https://qiita.com/MosamosaPoodle/items/8dc818191d59548b48c7) edit this file: `/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.13.sdk/usr/lib/libSystem.B.tbd`  to remove ` /usr/lib/system/libsystem_darwin.dylib,` from line #18

After that I was able to `bundle install` to completion and boot the rails application