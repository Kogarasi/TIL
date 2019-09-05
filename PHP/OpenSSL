# OpenSSL

## openssl_encryptの罠

こいつは厄介なやつ。
みんなkeyの部分にpassを入れて使っている・・・。こいつはkeyだぞ。
さらにkeyに関してはZero-Paddingされる。
けど、吐き出されるデータに関してはPKCS-7なので気を付けないといけない。

**openssl_encrypt ( string $data , string $method , string $key [, int $options = 0 [, string $iv = "" [, string &$tag = NULL [, string $aad = "" [, int $tag_length = 16 ]]]]] ) : string**
