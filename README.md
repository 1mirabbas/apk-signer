# APK Signing Script

A bash script to sign Android APK files with a self-generated keystore.

## Prerequisites

Make sure you have the following tools installed:
- `keytool` (comes with Java JDK)
- `jarsigner` (comes with Java JDK)
- `zipalign` (comes with Android SDK Build Tools)
- `apksigner` (comes with Android SDK Build Tools)

## Usage

```bash
./signing.sh <APK_NAME> <PASSWORD>
```

### Parameters

- `APK_NAME`: The name of the unsigned APK file you want to sign
- `PASSWORD`: The password to use for the keystore (minimum 6 characters)

### Example

```bash
./signing.sh unsigned_tg.apk testtest
```

## What the Script Does

1. **Validates Input**: Checks if the APK file exists and parameters are provided
2. **Cleans Up**: Removes any previous signing files
3. **Generates Keystore**: Creates a new keystore with RSA 2048-bit key
4. **Signs APK**: Signs the APK using jarsigner
5. **Aligns APK**: Optimizes the APK with zipalign for better performance
6. **Signs with apksigner**: Applies final signature
7. **Verifies**: Confirms the APK is properly signed and aligned

## Output

The script will generate:
- `signed_<APK_NAME>.apk` - Your signed APK file
- `android-app-hack-<APK_NAME>.keystore` - The generated keystore
- `signed_<APK_NAME>.apk.idsig` - Signature file

## Error Handling

The script will exit with an error message if:
- Parameters are missing
- APK file doesn't exist
- Any step in the signing process fails

## Important Notes

⚠️ **Keep your keystore and password secure!** You'll need the same keystore to sign updates to your app.

⚠️ **The keystore is valid for 365 days.** After that, you'll need to generate a new one.

## License

Free to use and modify.

