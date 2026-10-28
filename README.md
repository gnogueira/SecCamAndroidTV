# SecCamAndroidTV

Aplicativo para Android TV que mostra câmeras de NVRs compatíveis pela rede local. Suporta até 16 canais na interface, layouts lado a lado, empilhado e mosaico, tela cheia e tentativas de reconexão. A capacidade real depende do NVR, da rede e da TV.

A conexão usa o formato de substream RTSP dos NVRs Xiongmai/XMeye; outros protocolos e aparelhos precisam ser testados. Configure IP, porta, usuário e senha no aplicativo. A senha é criptografada com Android Keystore. As credenciais são usadas na conexão RTSP, portanto utilize uma rede confiável.

O identificador do aplicativo foi mantido para permitir atualização de instalações anteriores quando assinadas com a mesma chave. O número de sessões disponíveis no NVR também é compartilhado com outros dispositivos.

O código próprio usa [MIT](LICENSE). Consulte [THIRD_PARTY.md](THIRD_PARTY.md) para as licenças de componentes incorporados antes de distribuir um APK.

Abra esta pasta no Android Studio com JDK 17 e Android SDK 36, ou compile com:

```sh
./gradlew :app:assembleDebug
```

O APK debug resultante fica em `app/build/outputs/apk/debug/`, salvo quando se define `CAMTV_BUILD_DIR`. Um release sem assinatura pode ser gerado com `./gradlew :app:assembleRelease`. Para atualizar uma instalação existente, assine com a mesma chave usada na instalação anterior; não compartilhe essa chave.

A biblioteca `org.videolan.android:libvlc-all:3.7.7` é obtida dos repositórios configurados no Gradle. O pacote suporta ARMv7 e ARM64, Android 8.0 ou superior. A capacidade de decodificação varia entre TVs.

Teste das regras independentes de Android:

```sh
mkdir -p /tmp/camtv-tests
javac -encoding UTF-8 -d /tmp/camtv-tests app/src/main/java/br/com/camxp/tv/Model.java tests/ModelTest.java
java -cp /tmp/camtv-tests br.com.camxp.tv.ModelTest
```

Os testes de modelo não substituem testar reprodução, layouts, reconexão e navegação no aparelho real.
