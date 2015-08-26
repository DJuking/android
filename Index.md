Android WebView 调用Skype
===
Android代码调用：
Intent skypeVideoIntent = new Intent("android.intent.action.VIEW");
skypeVideoIntent.setData(Uri.parse("skype:d_juking?call&video=true"));
startActivity(skypeVideo);