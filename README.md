# sunmi_printer_plus (maintained fork)

> **This is a maintained fork of [brasizza/sunmi_printer](https://github.com/brasizza/sunmi_printer).**  
> The fork is maintained by [@abellido](https://github.com/abellido) with dependency upgrades, new features and bug fixes targeting Sunmi devices.
>
> **Branch status:**
> - `master` — mirrors the production-ready `version-4.0` branch plus documentation updates (this branch).
> - `version-4.0` — the active production branch where development takes place. If you are consuming the package directly from this repository, point your dependency to this branch.

---

## Important

**THIS PACKAGE WILL WORK ONLY IN ANDROID!**

This Flutter plugin is based on the Official Sunmi Inner Printer documentation using the latest implementation libs: [Sunmi Developer Documentation](https://developer.sunmi.com/docs/en-US/xeghjk491/mafeghjk535).

## Installation

Add the package to your `pubspec.yaml`.  
If you consume it from **pub.dev** (when published):

```yaml
dependencies:
  sunmi_printer_plus: ^4.1.1
```

Or install it via the Flutter CLI:

```bash
flutter pub add sunmi_printer_plus
```

To consume directly from this fork (recommended while pub.dev is not updated):

```yaml
dependencies:
  sunmi_printer_plus:
    git:
      url: https://github.com/abellido/sunmi_printer.git
      ref: version-4.0
```

Then run:

```bash
flutter pub get
```

## What this package does
- [x] Write some text (with style or not!)
- [x] Change font size
- [x] Jump (n) lines
- [x] Draw a divisor line
- [x] Bold mode on/off
- [x] Print all types of Barcodes (see enum below)
- [x] Print Qrcodes with custom width and error-level
- [x] Print image from asset or from web (example show how to print both)
- [x] Print rows like recepit with custom width and alignment
- [x] Able to combine with some esc/pos code that you already have!
- [x] Cut paper - Dedicated method just to cut the line
- [x] Printer serial no - Get the serial number of the printer
- [x] Printer version - Get the printer's version
- [x] Printer paper size - Get the paper size ( 0: 80mm 1: 58mm)
- [x] LCD Print a image  
- [x] LCD Print a string
- [x] Open de cash drawer 
- [x] Check if the cash drawer is open of close

# Run the example project

Clone this fork and switch to the `version-4.0` branch:

```bash
git clone https://github.com/abellido/sunmi_printer.git
cd sunmi_printer
git checkout version-4.0
cd example && flutter run
```

![Logo](https://github.com/brasizza/sunmi_printer/blob/version-4.0/doc/screen.png?raw=true)

## Deprecated Methods (`@Deprecated`)

The following methods have been kept for compatibility reasons but will be removed in future releases. Avoid using them in new implementations:

- `SunmiPrinter.initPrinter()`
- `SunmiPrinter.bold()`
- `SunmiPrinter.resetBold()`
- `SunmiPrinter.printRawData(Uint8List data)` → Use `printEscPos()` instead
- `SunmiPrinter.setCustomFontSize(int size)`
- `SunmiPrinter.setAlignment(dynamic align)`
- `SunmiPrinter.resetFontSize()`
- `SunmiPrinter.setFontSize(dynamic size)`
- `SunmiPrinter.startTransactionPrint(bool trans)`
- `SunmiPrinter.exitTransactionPrint(bool trans)`
- `SunmiPrinter.bindingPrinter()`
- `SunmiPrinter.cut()` → Use `cutPaper()` instead


# **You can also combine this package with the package [esc_pos_utils](https://pub.dev/packages/esc_pos_utils)**

_With this package you  **can**  create a custom escpos and than you don't need to use any other command.
This is good if you already have a code that another printers use, and u can reuse this code as well_ 

```dart
// import packages
import 'package:sunmi_printer_plus/sunmi_printer_plus.dart';




```
## Example code when use SunmiPrinter

```dart
        await SunmiPrinter.printText('Simple raw text');
        await SunmiPrinter.printText('Bold text centered',
            style: SunmiTextStyle(
            bold: true,
            align: SunmiPrintAlign.CENTER,
            ));

        await SunmiPrinter.lineWrap(2); // Jump 2 lines
        await SunmiPrinter.printText('Very Large font!',
            style: SunmiTextStyle(
            fontSize: 80,
            ));
                          
        await SunmiPrinter.printText('Custom font size!!!',
            style: SunmiTextStyle(
            fontSize: 32,
            ));
                          
        await SunmiPrinter.printQRCode(
            'https://github.com/brasizza/sunmi_printer',
            style: SunmiQrcodeStyle(
            qrcodeSize: 3,
            errorLevel: SunmiQrcodeLevel.LEVEL_H,
            )); // PRINT A QRCODE

```

# Example code for LCD functions 

```dart
await SunmiLcd.configLCD(SunmiLCDStatus)
 await SunmiLcd.lcdString('Hello'); //Write a simple line 
 await SunmiLcd.lcdString('Hello' , 12 , true); //Write a simple line with 12 in size and fill screen

 Uint8List byte = await readFileBytes('assets/images/128x40.png');
 await SunmiLcd.lcdImage(byte); // Put an image in LCD

```
# Example to open the cashier 

```dart
  bool await SunmiDrawer.i.isDrawerOpen(); //check if the cash drawer is connect or disconnect

  await SunmiDrawer.i.openDrawer(); //open de cash drawer


 ```

### List of enum printer mode

```dart
enum PrinterMode {
  NORMAL_MODE,
  BLACK_LABEL_MODE, 
  LABEL_MODE
}
```

### List of enum Alignments
```dart
enum SunmiPrintAlign {
  LEFT,
  CENTER,
  RIGHT,
}
```

### List of enum Qrcode levels
```dart
enum SunmiQrcodeLevel {
  LEVEL_L,
  LEVEL_M,
  LEVEL_Q,
  LEVEL_H,
}
```

### List of enum Barcode types
```dart
enum SunmiBarcodeType {
  UPCA,
  UPCE,
  JAN13,
  JAN8,
  CODE39,
  ITF,
  CODABAR,
  CODE93,
  CODE128,
}
```


### List of enum Text position in barcode
```dart
enum SunmiBarcodeTextPos {
  NO_TEXT,
  TEXT_ABOVE,
  TEXT_UNDER,
  BOTH,
}
```


### List of enum Font sizes
```dart
enum SunmiFontSize {
  XS,
  SM,
  MD,
  LG,
  XL,
}
```

### List of enum SunmiLCDStatus
```dart
enum SunmiLCDStatus {
  INIT,
  WAKE,
  SLEEP,
  CLEAR,
}
```

---

## Fork notice / Attribution

This repository is a maintained fork of [brasizza/sunmi_printer](https://github.com/brasizza/sunmi_printer), originally created and licensed by **Tan Zi Gang** and contributors under the **BSD 3-Clause License**.

All original copyright notices are preserved in the `LICENSE` file. The fork introduces dependency upgrades, code refactors, new printer/drawer methods, and improved documentation. See `CHANGELOG.md` for details.

Upstream repository: <https://github.com/brasizza/sunmi_printer>  
License: [BSD 3-Clause](./LICENSE)

---

## License

BSD 3-Clause License. See [LICENSE](./LICENSE) for the full text.
