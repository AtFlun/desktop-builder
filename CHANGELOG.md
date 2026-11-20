# 变更日志

## [6.6.5] - 2026-11-20 21:40
### 优化
- 优化了一些细节;

## [6.6.4] - 2026-11-20 20:52
### 修复
- 修复 `nativeModules.npmRebuild` 合并 `allowScripts` 的块未受重装条件约束的问题:该块此前写在重装判断之外,
  `[信息] 跳过安装与优化` 分支下仍会扫描 `node_modules`、打印原生模块提示并回写 `package.json`;
- 该块移入 `if (shouldInstall)` 分支内、`npm install` 之前,内层条件简化为 `npmRebuildCfg`,
  仅在确实重装依赖时并入白名单并打印提示;
### 优化
- `allowScripts` 合并的遍历合二为一:先按 `@scope` 生成候选包名数组(`@scope/sub` 或单个包名),
  再统一检查 `binding.gyp` 与白名单,消除两段几乎相同的分支;
- 逻辑随 `if (shouldInstall)` 下移后,不再需要 `npmRebuildCfg && shouldInstall` 短路判断,
  代码结构与「是否重装」一一对应;

## [6.6.3] - 2026-11-20 19:29
### 新增
- `nativeModules.npmRebuild` 开启时,安装依赖前扫描用户项目 `node_modules`(含 `@scope` 子目录)中带 `binding.gyp` 的包,
  无条件并入根 `package.json` 的 `allowScripts`,使 `npm install` 放行其 install 脚本;传递依赖中的原生模块(如 `bcrypt`)一并覆盖;
- 仅在确有新增时回写,并打印绿色提示 `原生模块[<包名>, ...]无条件加入allowScripts白名单`,多个模块合并为一行、逗号分隔;