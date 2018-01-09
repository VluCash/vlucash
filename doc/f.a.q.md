===============================Trouble Shoot Installation===============================
Q : can't make....
A : you need some plugin or addon for fresh installation

go terminal copy and right click paste on terminal:

apt install build-essential libqt4-dev qt5-qmake cmake qttools5-dev libqt5webkit5-dev qttools5-dev-tools qt5-default python-sphinx texlive-latex-base inotify-tools  openssl libssl-dev libdb++-dev libminiupnpc-dev git sqlite3 libsqlite3-dev g++ libpng-dev git g++ gedit python gcc make libbz2-dev libdb-dev libssl-dev openssl libreadline-dev autoconf libtool git libleveldb-dev libblkid-dev e2fslibs-dev libboost-all-dev libaudit-dev automake nano qtbase5-dev qt4-dev-tools libqt4-core libqt4-gui libqt5-core libqt5-gui

Q : got error like this

Building CXX object src/CMakeFiles/Common.dir/Common/Base58.cpp.o /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp: In function ¡®uint64_t Tools::Base58::{anonymous}::uint_8be_to_64(const uint8_t*, size_t)¡¯: /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:90:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 1: res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:91:9: note: here case 2: res <<= 8; res |= *data++; ^~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:91:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 2: res <<= 8; res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:92:9: note: here case 3: res <<= 8; res |= *data++; ^~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:92:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 3: res <<= 8; res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:93:9: note: here case 4: res <<= 8; res |= *data++; ^~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:93:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 4: res <<= 8; res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:94:9: note: here case 5: res <<= 8; res |= *data++; ^~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:94:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 5: res <<= 8; res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:95:9: note: here case 6: res <<= 8; res |= *data++; ^~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:95:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 6: res <<= 8; res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:96:9: note: here case 7: res <<= 8; res |= *data++; ^~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:96:32: error: this statement may fall through [-Werror=implicit-fallthrough=] case 7: res <<= 8; res |= *data++; ~~~~^~~~~~~~~~ /home/meric/Desktop/WayangCli-master(1)/WayangCli-master/src/Common/Base58.cpp:97:9: note: here case 8: res <<= 8; res |= *data; break; ^~~~ cc1plus: all warnings being treated as errors src/CMakeFiles/Common.dir/build.make:62: recipe for target 'src/CMakeFiles/Common.dir/Common/Base58.cpp.o' failed make[3]: *** [src/CMakeFiles/Common.dir/Common/Base58.cpp.o] Error 1 make[3]: Leaving directory '/home/meric/Desktop/WayangCli-master(1)/WayangCli-master/build/release' CMakeFiles/Makefile2:515: recipe for target 'src/CMakeFiles/Common.dir/all' failed make[2]: *** [src/CMakeFiles/Common.dir/all] Error 2 make[2]: Leaving directory '/home/meric/Desktop/WayangCli-master(1)/WayangCli-master/build/release' Makefile:94: recipe for target 'all' failed make[1]: *** [all] Error 2 make[1]: Leaving directory '/home/meric/Desktop/WayangCli-master(1)/WayangCli-master/build/release' Makefile:20: recipe for target 'build-release' failed make: *** [build-release] Error 2

A : try change src/CryptoNoteConfig.h like this

see line

const uint64_t MONEY_SUPPLY = UINT64_C(1000000);

change to

const uint64_t MONEY_SUPPLY = (uint64_t)(-1);

Q : Genesis block transaction
A : you can empty first this line on src/CryptoNoteConfig.h

const char     GENESIS_COINBASE_TX_HEX[]                     = "010a01ff0001904e029b2e4c0281c0b02e7c53291a94d1d0cbff8883f8024f5142ee494ffbbd08807121018b64cdddcc1eecbed35ab64855279f5635ebb681f1812f51af2ed083bc4b457e";

to this

const char     GENESIS_COINBASE_TX_HEX[]                     = "";

Generate by make and try run daemon

[daemon name] —print-genesis-tx

and Copy the genenis to

const char     GENESIS_COINBASE_TX_HEX[]                     = "[genesis code when generated";

Q : i wanna hard fork from your block chain how
A : easy just input on this on src/CryptoNoteConfig.h

const std::initializer_list<CheckpointData> CHECKPOINTS = {
    //{ 1, "cbce7c37dbad257d29a3bfa93ec1f7b92434b9b806d40d01cb04d0ad2e451735" },    
};

to

const std::initializer_list<CheckpointData> CHECKPOINTS = {
    { 1, "[checkpoint block see on checkpoint list]" },  
};  

Q : getting error debian CMAKE...
A : try used this constume kenel https://drive.google.com/open?id=1-Zn5keAhyNc8WajsKKznMD5vbRYaDWnD
    try this command dpkg -i linux-image-4.14.8-kohakuv1_4.14.8-kohakuv1-10.00.Custom_amd64.deb
