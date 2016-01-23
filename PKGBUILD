pkgname=samsung-uld-printer
pkgver=1.00.36_00.91
pkgrel=1
pkgdesc="Samsung Universal Driver (printers only)"
arch=('x86_64')
license=('custom')
depends=('cups')
source=("http://org.downloadcenter.samsung.com/downloadfile/ContentsFile.aspx?CDSite=US&CttFileID=6285111&CDCttType=DR&ModelType=C&ModelName=ML-2165W/XAC&VPath=DR/201510/20151028120356557/uld_v1.00.36_00.91.tar.gz")
md5sums=('ba1d213aa726efaf20c1b31f4da9fcdc')

package() {
    cd "uld"
    INSTDIR_COMMON_PRINTER_LIB="/usr/lib"
    INSTDIR_CUPS_BIN="/usr/lib/cups"
    INSTDIR_CUPS_FILTERS="$INSTDIR_CUPS_BIN/filter"
    INSTDIR_CUPS_BACKENDS="$INSTDIR_CUPS_BIN/backend"

    mkdir -p "$pkgdir$INSTDIR_CUPS_FILTERS"
    mkdir -p "$pkgdir$INSTDIR_CUPS_BACKENDS"

    install -m 755 "x86_64/rastertospl" "$pkgdir$INSTDIR_CUPS_FILTERS"
    install -m 755 "x86_64/pstosecps" "$pkgdir$INSTDIR_CUPS_FILTERS"
    install -m 755 "x86_64/smfpnetdiscovery" "$pkgdir$INSTDIR_CUPS_BACKENDS"
    install -m 755 "x86_64/libscmssc.so" "$pkgdir$INSTDIR_COMMON_PRINTER_LIB"

    INSTDIR_PPD="$pkgdir/usr/share/ppd/samsung"
    PKGDIR_PPD="noarch/share/ppd/*.ppd"
    PKGDIR_CMS="noarch/share/ppd/cms/*.cts"
    for f in $PKGDIR_PPD
    do
        install -m 644 -D $f "$INSTDIR_PPD/$(basename $f)"
    done
    for f in $PKGDIR_CMS
    do
        install -m 644 -D $f "$INSTDIR_PPD/cms/$(basename $f)"
    done

    install -m 644 -D "noarch/license/eula.txt" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

