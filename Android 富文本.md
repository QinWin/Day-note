
====================================================================
### 富文本实现

1. SpannableString 

~~~
        String pa = getString(R.string.protocol_yoonuu);
        SpannableString ss = new SpannableString(pa);
        ss.setSpan(new ClickableSpan() {
            @Override
            public void onClick(@NonNull View widget) {
                Intent intent = new Intent(LoginActivity.this, ProtocolActivity.class);
                startActivityForResult(intent, 0x101);
            }

            @Override
            public void updateDrawState(@NonNull TextPaint ds) {
                super.updateDrawState(ds);
                   //下划线取消
                ds.setUnderlineText(false);
            }
        },5, ss.length(), Spanned.SPAN_MARK_MARK);
        ss.setSpan(new ForegroundColorSpan(getResources().getColor(R.color.lgn_protocol)), 5, ss.length(), Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        mProtocol.setMovementMethod(LinkMovementMethod.getInstance());
        mProtocol.setText(ss);
        //默认同意协议
        mProtocol.setActivated(true);
~~~

2.温度符号
In xml.file for Celsius

android:text="\u2103"
for Fahrenheit

android:text="\u2109"
for Kelvin

android:text="\u212A"
for Romer

android:text="\u00B0R"

3.空格
空格：&#160;（普通的英文半角空格但不换行）
窄空格：&#8201;
&#12288;（中文全角空格 （一个中文宽度））
&#8194;（半个中文宽度，但两个空格比一个中文略大）
&#8195;（一个中文宽度，但用起来会比中文字宽一点点）
\u3000\u3000（首行缩进）
\u3000（全角空格(中文符号)）
\u0020（半角空格(英文符号)）
&#8230;（省略号）