# 京东微信域界面动效语言

一个参数化的动效语言 skill，用于把动效设计意图转译为京东微信域产品中的具体参数。

## 定位

- 上层输入：来自 `jd-motion-principles` 等 12 法则基础 skill 的场景性格和情绪方向。
- 本层作用：输出京东品牌下的坐标系、运动模式、时长、缓动曲线和编排规则。
- 下层输出：供 Lottie / CSS / Motion / GSAP 等执行 skill 渲染实现。

## 覆盖范围

- 坐标系：X / Y / Z 三轴
- 运动类型：微观（micro）与宏观（macro）
- 运动模式：轴运动、容器转换、淡入淡出
- 场景分类：平台场景（platform）与互动场景（campaign）
- 时长表与缓动表
- 编排规则

## 目录结构

```
jd-jd-motion-language/
├── SKILL.md                      # 核心入口
├── README.md                     # 本文件
├── LICENSE                       # MIT
├── examples/                     # 示例
│   ├── .gitkeep
│   └── jd-motion-pipeline.yml    # 京东动效调用流程
└── references/                   # 详细参数表
    ├── timing-table.md
    ├── easing-table.md
    ├── axis-mapping.md
    ├── composition-rules.md
    └── framework-mapping.md
```

## 使用方式

### 推荐：与 jd-motion-principles 串行使用

本 skill 是**参数层**，上游建议由 `jd-motion-principles` 先完成判断：

```
用户需求 → jd-motion-principles（判断层）→ jd-jd-motion-language（参数层）→ 执行 skill → jd-motion-principles（审查层）
```

1. 先用 `jd-motion-principles` 判断场景性格、情绪方向、元素层级和反模式。
2. 再调用本 skill，输入判断结果，输出京东微信域坐标/时长/曲线/编排参数。
3. 执行 skill（Lottie / CSS / Motion / GSAP）生成最终动效。
4. 最后用 `jd-motion-principles` 审查输出是否违反反模式。

具体示例见 `examples/jd-motion-pipeline.yml`。

### 单独使用

当需求已经非常明确时，可直接调用本 skill 输出参数：

```yaml
input:
  scene: platform
  motion: 弹窗从底部进入
  axis: Y
  type: macro
output:
  duration_ms: 140
  easing: cubic
```

