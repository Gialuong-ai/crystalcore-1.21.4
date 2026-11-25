# CrystalCore – Fabric client mod (Minecraft 1.21.4, Java 21, Yarn)

## Cấu trúc
```
src/main/java/dev/crystalcore/
  CrystalCore.java            entrypoint, nối tick/HUD/world-render vào EventBus
  event/    EventBus, Events  (Tick, Render3D, Render2D, AttackEntity(+Post), InteractBlock)
  module/   Module, Category, ModuleManager
    modules/ CrystalAura, CrystalOptimizer, Surround, AutoTotem, CrystalProtect, ESP, HudModule
  setting/  Setting, BoolSetting, NumberSetting, EnumSetting
  config/   ConfigManager     -> .minecraft/config/crystalcore.json
  gui/      ClickGuiScreen    (Right Shift)
  util/     DamageUtil, CrystalUtil, BlockUtil, InventoryUtil, RotationUtil, RenderUtil, ActionGuard
  mixin/    ClientPlayerInteractionManagerMixin, EntityMixin
src/main/resources/ fabric.mod.json, crystalcore.mixins.json, lang
```

## Build
1. Cần JDK 21. Tạo Gradle wrapper một lần (repo này chưa kèm gradle-wrapper.jar):
   - Có Gradle sẵn: `gradle wrapper --gradle-version 8.11.1`
   - Hoặc tải template tại https://fabricmc.net/develop rồi chép `gradlew`, `gradlew.bat`,
     `gradle/wrapper/gradle-wrapper.jar` vào thư mục này.
   - Hoặc mở project bằng IntelliJ IDEA và chạy task `build`.
2. Build:  `./gradlew build`   (Windows: `gradlew.bat build`)
3. Lấy file **`build/libs/crystalcore-1.0.0.jar`** (đã remap sang intermediary) bỏ vào `.minecraft/mods/`.
   - KHÔNG dùng `crystalcore-1.0.0-dev.jar` (nằm ở `build/devlibs/`, chưa remap, sẽ crash khi chạy thật).
   - `crystalcore-1.0.0-sources.jar` chỉ là mã nguồn.
4. Cần Fabric Loader >= 0.16 và Fabric API cho 1.21.4. Test nhanh: `./gradlew runClient`.

Nếu Gradle báo không tìm thấy phiên bản Fabric API/Loader/Yarn, sửa số phiên bản trong
`gradle.properties` theo https://fabricmc.net/develop.

## Dùng
- Right Shift: mở ClickGUI. Chuột trái bật/tắt, chuột phải mở setting, chuột giữa gán phím.
- Config tự lưu khi đóng GUI / thoát game.
