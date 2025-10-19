# Maintainer: copycat <simakr2512 | at | yandex [DOT] ru>
pkgname=('kompas3d-v24')
pkgver=24.1.0.64
pkgrel=1
arch=('x86_64')
pkgdesc='Proprietary russian CAD system'
url='https://sd.ascon.ru/otrs/customer.pl?Action=CustomerK3DBetaTesting'
license=('custom')
depends=('libc++' 'libunwind')
install=${pkgname}.install

source=( "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-common-v24/ascon-kompas-common-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-graphic-v24/ascon-kompas-graphic-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas3d-v24/ascon-kompas3d-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-help-v24/ascon-kompas-help-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-fonts/ascon-kompas-fonts_1.0.0.4_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-sdk-v24/ascon-kompas-sdk-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-coupling-v24/ascon-kompas-coupling-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-dimchain-v24/ascon-kompas-dimchain-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-servicetools-v24/ascon-kompas-servicetools-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-checker-v24/ascon-kompas-checker-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-featurekompas-v24/ascon-kompas-featurekompas-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-nesting-v24/ascon-kompas-nesting-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-libsamples-v24/ascon-kompas-libsamples-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon-kompas-plugins-v24/ascon-kompas-plugins-v24_24.1.0.64_amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/a/ascon/ascon-polynom-library-23.3-23.3.0.25091905-amd64.deb"
         "https://repo.ascon.ru/beta/deb/pool/main/g/grdcontrol/grdcontrol_4.3.0_amd64.deb")
noextract=("${source[@]##*/}")

sha256sums=('7b56ddd853795dbbb0ab68ef7f1536df44690514aeaff5a1909e233e940d2701'
            '6ce5f44fae11647c6a1a919f37c536847036916c5ea32fb1222cfe823aab7891'
            '33ffef27e95f44a8fce9c616d195174e5837ae706bd01059d6a2499f97d9b8d4'
            '5ace1108394629f4b46cdadcb798b8a4b3ad91e88f6987e54662db18754d6d71'
            '94d3c236b928cfadbe2c291aec0e9c8f52ec823e631557e4f40800aa3534b3bc'
            '0f5e0b807b6a7be06c20178291a25dcab363d94c72bd4d562ff6e17135bb406a'
            '0556dc647a3c683807c68a64c64d129450517248f0e7e1eb3d6dc15119b9be30'
            '1b662f0eae8822e446e8d38219b8d00b7d656453578d576f12eb311a7cc9b3c4'
            '1b7f92aaae5627b5e075bd311ae9457333ea18fb151a5821842acd8faf0ad6df'
            '26e1a194a9a57d96c3c48ff6bb37522bfc07e8105448ab12f56c69f7fe94dae1'
            '15233ce3cfb04ce03b3a5f382cfcc52c8e963fe798eed69228c445513e4d44e1'
            '4a247ccd31e2243d8807959d56f1a90b4044b6b0db5c92e38d30bcc58e4dd576'
            'fa94a8bf0cf78bd7a8de37ee76220e54953bf116fa0eaa268a5eaf58fbca0f6f'
            '57a855464bfc2a00ead8fd31f88574668c27832ea261a0d42f0a6bead0075452'
            '4c14101a78a09cbc549f84da773bfd6bac5ad546ab8ed316d4c0f8c011aadc1b'
            '353ce9eec8d4fcfe32b1d3b242274d0f0e87fcbf7ffcbab5b8d839fb756b9b27')

extract_deb() {
    debname=$1
    debdir=${debname%.*}

    mkdir -p $debdir

    echo Extracting $debname
    ar x --output $debdir $debname
    cd $debdir

    mkdir -p control
    cd control; tar -xf ../control.*; cd ..

    mkdir -p data
    cd data; tar -xf ../data.*; cd ..

    cd data; cp -R * $pkgdir/

    cd $srcdir
}

fixdeps(){
    #ignore those
    if [[ $1 == *"kompas-thumbnailer"* ]]; then
        return
    fi
    echo $1
    patchelf --replace-needed libunwind.so.1 libunwind.so $1
}

filterfile(){
    filetype=$(file -i "$1")
    #application/x-sharedlib; charset=binary
    #application/x-pie-executable; charset=binary
    #application/x-executable; charset=binary
    if [[ $filetype == *"application/x-sharedlib; charset=binary"* ]] || [[ $filetype == *"application/x-pie-executable; charset=binary"* ]] || [[ $filetype == *"application/x-executable; charset=binary"* ]]; then
        fixdeps $1
    fi
}

patchdebiandeps(){
    echo Patching ELFs
    cd $pkgdir

    #to make /usr/bin/file not crash
    OLD_LD_LIBRARY_PATH=$LD_LIBRARY_PATH
    OLD_LD_PRELOAD=$LD_PRELOAD
    export LD_LIBRARY_PATH=
    export LD_PRELOAD=

    find . -type f -print0 | while IFS= read -r -d '' file; do filterfile "$file"; done

    #revert build env
    export LD_LIBRARY_PATH=$OLD_LD_LIBRARY_PATH
    export LD_PRELOAD=$OLD_LD_PRELOAD
    cd $srcdir
}

package() {
    #for bsdtar, some filenames are in Russian
    export LC_ALL=ru_RU.UTF-8

    echo Repacking!
    for d in *.deb; do extract_deb $d ; done

    patchdebiandeps

    cd $srcdir
}
