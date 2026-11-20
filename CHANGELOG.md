# 变更日志

## [6.6.3] - 2026-11-20 19:29
### 新增
- `nativeModules.npmRebuild` 开启时,安装依赖前扫描用户项目 `node_modules`(含 `@scope` 子目录)中带 `binding.gyp` 的包,
  无条件并入根 `package.json` 的 `allowScripts`,使 `npm install` 放行其 install 脚本;传递依赖中的原生模块(如 `bcrypt`)一并覆盖;
- 仅在确有新增时回写,并打印绿色提示 `原生模块[<包名>, ...]无条件加入allowScripts白名单`,多个模块合并为一行、逗号分隔;

## [6.6.2] - 2026-11-13 20:37
### 更新
- 依赖包更新;

## [6.6.1] - 2026-11-09 16:47
### 优化
- 细节优化;