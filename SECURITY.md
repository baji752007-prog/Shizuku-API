private void onRequestPermissionsResult(int requestCode, int grantResult) {
    boolean granted = grantResult == PackageManager.PERMISSION_GRANTED;
    // Do stuff based on the result and the request code
}

private final Shizuku.OnRequestPermissionResultListener REQUEST_PERMISSION_RESULT_LISTENER = this::onRequestPermissionsResult;

@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...
    Shizuku.addRequestPermissionResultListener(REQUEST_PERMISSION_RESULT_LISTENER);
    // ...
}

@Override
protected void onDestroy() {
    // ...
    Shizuku.removeRequestPermissionResultListener(REQUEST_PERMISSION_RESULT_LISTENER);
    // ...
}

private boolean checkPermission(int code) {
  if (Shizuku.isPreV11()) {
    // Pre-v11 is unsupported
    return false;
  }

  if (Shizuku.checkSelfPermission() == PackageManager.PERMISSION_GRANTED) {
    // Granted
    return true;
  } else if (Shizuku.shouldShowRequestPermissionRationale()) {
    // Users choose "Deny and don't ask again"
    return false;
  } else {
    // Request the permission
    Shizuku.requestPermission(code);
    return false;
  }
}
# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.
