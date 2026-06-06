<template>
  <div class="instruction-page">
    <header class="instruction-header">
      <nav class="instruction-nav" aria-label="页面导航">
        <RouterLink to="/home" class="instruction-brand" aria-label="返回首页">
          <img src="/logo.png" alt="AIChatGPT" />
          <span>
            <strong>AIChatGPT</strong>
            <small>Codex 使用文档</small>
          </span>
        </RouterLink>
        <div class="instruction-actions">
          <a href="#quickChecklist" class="instruction-link">
            <Icon name="checkCircle" size="sm" />
            快速检查
          </a>
          <a :href="registerUrl" target="_blank" rel="noopener noreferrer" class="instruction-primary-link">
            <Icon name="externalLink" size="sm" />
            打开注册页
          </a>
        </div>
      </nav>
    </header>

    <div class="instruction-frame">
      <aside class="instruction-toc" aria-label="教程目录">
        <div class="instruction-toc-heading">
          <Icon name="book" size="md" />
          <div>
            <strong>教程目录</strong>
            <span>点击章节跳转</span>
          </div>
        </div>
        <nav>
          <section>
            <p>页面概览</p>
            <a href="#guideTitle"><Icon name="chevronRight" size="xs" />教程总览</a>
            <a href="#readingGuide"><Icon name="chevronRight" size="xs" />阅读指南</a>
          </section>
          <section>
            <p>第一章 准备工作</p>
            <a href="#notice"><Icon name="chevronRight" size="xs" />使用前说明</a>
            <a href="#register"><Icon name="chevronRight" size="xs" />注册中转账户</a>
            <a href="#billing"><Icon name="chevronRight" size="xs" />充值与订阅</a>
            <a href="#redeem"><Icon name="chevronRight" size="xs" />兑换中转码</a>
          </section>
          <section>
            <p>第二章 创建 API 密钥</p>
            <a href="#createKey"><Icon name="chevronRight" size="xs" />创建新密钥</a>
            <a href="#configPreview"><Icon name="chevronRight" size="xs" />接入配置预览</a>
          </section>
          <section>
            <p>第三章 Codex 接入</p>
            <a href="#installCodex"><Icon name="chevronRight" size="xs" />手动配置 Codex</a>
            <a href="#configureCodex"><Icon name="chevronRight" size="xs" />Windows 配置</a>
            <a href="#configureCodexMac"><Icon name="chevronRight" size="xs" />Mac 配置</a>
            <a href="#otherClientGuides"><Icon name="chevronRight" size="xs" />其他客户端</a>
            <a href="#loginCodex"><Icon name="chevronRight" size="xs" />重新登录 Codex</a>
          </section>
          <section>
            <p>第四章 验证与排错</p>
            <a href="#quickCheck"><Icon name="chevronRight" size="xs" />一行命令自检</a>
            <a href="#quickChecklist"><Icon name="chevronRight" size="xs" />登录失败检查</a>
            <a href="#troubleTable"><Icon name="chevronRight" size="xs" />常见报错对照</a>
          </section>
          <section>
            <p>第五章 FAQ</p>
            <a href="#faq"><Icon name="chevronRight" size="xs" />常见问题</a>
          </section>
        </nav>
      </aside>

      <main class="instruction-shell">
        <section class="instruction-hero" aria-labelledby="guideTitle">
          <p class="instruction-base">API base_url: {{ baseUrl }}</p>
          <h1 id="guideTitle">兑换中转 API Key，并接入 Codex</h1>
          <p>
            从注册中转账户、兑换中转码、创建 API 密钥，到手动接入 Codex 和常见排错。
            Claude Code、Open Code、Open Claw 和移动端客户端也可以参照“使用密钥”弹窗里的对应配置。
          </p>
          <div class="instruction-badges" aria-label="教程要点">
            <span><Icon name="gift" size="sm" />先兑换中转码</span>
            <span><Icon name="key" size="sm" />生成 API Key</span>
            <span><Icon name="cog" size="sm" />手动配置 Codex</span>
            <span><Icon name="chat" size="sm" />排错与自检</span>
          </div>
          <nav class="instruction-jump" aria-label="章节快捷入口">
            <a href="#chapterPrepare">准备</a>
            <a href="#chapterKey">拿 Key</a>
            <a href="#installCodex">手动配置</a>
            <a href="#chapterTrouble">验证排错</a>
          </nav>
        </section>

        <article class="instruction-article">
          <h1>Codex API 登录对接教程</h1>

          <section class="instruction-callout instruction-callout-important" aria-label="站点信息卡">
            <p><strong>重要｜站点信息卡</strong></p>
            <div class="instruction-table-wrap">
              <table class="instruction-table">
                <tbody>
                  <tr>
                    <th>中转注册页</th>
                    <td>
                      <a :href="registerUrl" target="_blank" rel="noopener noreferrer">{{ registerUrl }}</a>
                    </td>
                  </tr>
                  <tr>
                    <th>个人资料额度查询页</th>
                    <td>
                      <a :href="profileUrl" target="_blank" rel="noopener noreferrer">{{ profileUrl }}</a>
                    </td>
                  </tr>
                  <tr>
                    <th>卡密自助购买地址</th>
                    <td>
                      <a href="https://pay.ldxp.cn/shop/LSSZLMUY" target="_blank" rel="noopener noreferrer">
                        https://pay.ldxp.cn/shop/LSSZLMUY
                      </a>
                    </td>
                  </tr>
                  <tr>
                    <th>推荐客户端</th>
                    <td>可手动接入 Codex APP / Codex CLI / Codex VSCode 插件。</td>
                  </tr>
                  <tr>
                    <th>订阅模式</th>
                    <td>每天有一定额度，每天 0 点后自动刷新。</td>
                  </tr>
                  <tr>
                    <th>额度模式</th>
                    <td>使用时消耗网站账户里的额度，用完就没有了。</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </section>

          <h2 id="readingGuide">阅读指南</h2>
          <p>
            本教程把使用流程拆成 <strong>“准备 → 拿 Key → 手动配置 → 验证”</strong> 四步。
            无论是通过质保兑换补发的中转兑换码，还是在链动小铺购买的额度包兑换码，都适用以下流程。
          </p>
          <div class="instruction-table-wrap">
            <table class="instruction-table">
              <thead>
                <tr>
                  <th>你的身份</th>
                  <th>阅读路径</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>第一次使用，从零开始</td>
                  <td>第一章 → 第二章 → 第三章手动配置 → 第四章</td>
                </tr>
                <tr>
                  <td>已有中转账号，只想配置某个客户端</td>
                  <td>第二章 → 第三章；其他客户端请参考对应客户端弹窗配置。</td>
                </tr>
                <tr>
                  <td>配置后登录失败或限额</td>
                  <td>第四章验证与排错</td>
                </tr>
              </tbody>
            </table>
          </div>

          <section class="instruction-callout instruction-terms" aria-label="名词速懂">
            <p><strong>提示｜名词速懂</strong></p>
            <ul>
              <li>
                <strong>base_url：</strong>
                中转站的前台地址，告诉客户端去哪请求 AI。本教程默认使用
                <code>{{ baseUrl }}</code>，部分 OpenAI-compatible 客户端需要按弹窗填写
                <code>/v1</code> 后缀。
              </li>
              <li>
                <strong>api_key：</strong>
                你的“门票”，形如 <code>sk-xxxx</code>，用于区分用户与记录消费；不能泄露。
              </li>
              <li>
                <strong>sub2api：</strong>
                把订阅式服务转换为可被代码或客户端调用的 API，本教程中的兑换码和订阅权益都可理解为这个接入链路的一部分。
              </li>
            </ul>
          </section>

          <hr />

          <h1 id="chapterPrepare">第一章 准备工作</h1>
          <h2 id="notice">1.1 使用前说明</h2>
          <p>Codex App 是 GPT 官方推出的软件，具备网页版的核心能力，并且在本地客户端中提供更强的使用体验。</p>

          <div class="instruction-alert instruction-alert-info">
            <Icon name="questionCircle" size="md" />
            <div>
              <strong>兑换码来源都适用。</strong>
              <span>本教程同时适用于按邮箱质保剩余时间补发的中转兑换码，以及在链动小铺购买的额度包兑换码。</span>
            </div>
          </div>

          <div class="instruction-card-grid" aria-label="API Key 分组选择规则">
            <article class="instruction-card instruction-card-danger">
              <Icon name="exclamationTriangle" size="md" />
              <div>
                <strong>链动小铺额度包：必须选择 GPT 分组</strong>
                <span>链动小铺购买的额度包（不限时），新建 API Key 时必须选择 <code>GPT</code> 分组。</span>
              </div>
            </article>
            <article class="instruction-card instruction-card-warning">
              <Icon name="calendar" size="md" />
              <div>
                <strong>链动小铺订阅包：选择对应订阅分组</strong>
                <span>链动小铺购买的订阅包（不限时），新建 API Key 时选择你购买相应的额度分组。</span>
              </div>
            </article>
            <article class="instruction-card instruction-card-success">
              <Icon name="shield" size="md" />
              <div>
                <strong>质保补发码：选择质保补偿</strong>
                <span>通过质保网站补发的中转兑换码，在新建 API Key 时选择“质保补偿”分组。</span>
              </div>
            </article>
          </div>

          <div class="instruction-two-grid" aria-label="计费模式提醒">
            <article>
              <Icon name="clock" size="md" />
              <div>
                <strong>订阅模式</strong>
                <span>每天有一定额度，每天 0 点后自动刷新。</span>
              </div>
            </article>
            <article>
              <Icon name="dollar" size="md" />
              <div>
                <strong>额度模式</strong>
                <span>使用时消耗网站账户里的额度，用完就没有了。</span>
              </div>
            </article>
          </div>

          <div class="instruction-support-grid">
            <article class="instruction-support-card">
              <strong>需要额外购买卡密？</strong>
              <span>可通过链动小铺自助购买额度包兑换码。</span>
              <a href="https://pay.ldxp.cn/shop/LSSZLMUY" target="_blank" rel="noopener noreferrer" class="instruction-primary-link">
                <Icon name="creditCard" size="sm" />
                打开卡密自助购买地址
              </a>
            </article>
            <figure class="instruction-figure instruction-qr">
              <img src="/img/codex-guide/image-16.png" alt="问题交流群二维码" loading="lazy" />
              <figcaption>有任何问题请扫码加群，联系群主处理。</figcaption>
            </figure>
          </div>

          <h2 id="register">1.2 注册中转账户</h2>
          <p>
            <strong>操作步骤：</strong>
            浏览器打开中转注册链接，填写邮箱、获取验证码、设置密码后完成注册。
          </p>
          <a :href="registerUrl" target="_blank" rel="noopener noreferrer" class="instruction-inline-link">
            <Icon name="externalLink" size="sm" />
            {{ registerUrl }}
          </a>
          <figure class="instruction-figure">
            <img src="/img/codex-guide/image.png" alt="中转服务注册页面截图" loading="lazy" />
            <figcaption>图 1：注册页面，输入邮箱、密码和验证码后创建账户。</figcaption>
          </figure>

          <h2 id="billing">1.3 充值与订阅</h2>
          <p>如果账号内还没有可用权益，可通过站内充值 / 订阅、卡密自助购买，或兑换已发放的中转兑换码获得额度。</p>
          <ul class="instruction-steps-list">
            <li><strong>充值模式：</strong>按金额充值，按调用量从余额中扣费。</li>
            <li><strong>订阅模式：</strong>按天 / 月 / 季 / 年等周期提供固定额度，更适合稳定使用。</li>
            <li><strong>倍率与套餐：</strong>不同站点、不同分组可能不同，具体以中转后台实时显示为准。</li>
          </ul>
          <section class="instruction-callout">
            <p>
              <strong>注意：</strong>
              充值、订阅和兑换码都是权益来源；创建 API Key 时仍然要按“质保补偿 / GPT / 订阅分组”等选择规则来绑定正确权益。
            </p>
          </section>

          <h2 id="redeem">1.4 兑换中转码</h2>
          <p>
            登录后进入兑换页面
            <a :href="redeemUrl" target="_blank" rel="noopener noreferrer">{{ redeemUrl }}</a>，
            输入提供给你的中转兑换码或额度包兑换码，点击“兑换”。
          </p>
          <figure class="instruction-figure">
            <img src="/img/codex-guide/image-1.png" alt="兑换成功后的页面截图" loading="lazy" />
            <figcaption>图 2：兑换成功后，账户会获得对应余额或权益。</figcaption>
          </figure>
          <figure class="instruction-figure">
            <img src="/img/codex-guide/image-17.png" alt="中转账户最近活动显示订阅兑换记录" loading="lazy" />
            <figcaption>图 3：兑换记录会出现在最近活动中，可用于确认权益是否到账。</figcaption>
          </figure>

          <hr />

          <h1 id="chapterKey">第二章 创建 API 密钥（所有接入方式通用）</h1>
          <section class="instruction-callout instruction-callout-important">
            <p>
              <strong>重要｜本章是所有客户端的前置步骤。</strong>
              无论后面要接 Codex、Claude Code、Open Code 还是 Open Claw，都要先在这里拿到一把自己的 API Key。
            </p>
          </section>

          <h2 id="createKey">2.1 创建新密钥并选择正确分组</h2>
          <p>
            登录后进入
            <a :href="keysUrl" target="_blank" rel="noopener noreferrer">API 密钥页面</a>，
            点击“创建密钥”。名称可按自己需要填写，也建议按用途命名，例如
            <code>codex</code>、<code>claude-mac</code>、<code>opencode-win</code>，
            方便后续区分和单独吊销。
          </p>

          <div class="instruction-card-grid" aria-label="创建密钥计费模式提醒">
            <article class="instruction-card instruction-card-success">
              <Icon name="infoCircle" size="md" />
              <div>
                <strong>订阅类分组：质保补偿 / 订阅**</strong>
                <span>“质保补偿”和“订阅**”是订阅制度，不需要消耗余额；质保网站补发的中转码选“质保补偿”。</span>
              </div>
            </article>
            <article class="instruction-card instruction-card-danger">
              <Icon name="dollar" size="md" />
              <div>
                <strong>额度类分组：GPT</strong>
                <span>链动小铺购买余额包或额度包时，应选择 <code>GPT</code> 分组。创建密钥前请再次确认自己使用的是订阅还是额度。</span>
              </div>
            </article>
            <article class="instruction-card instruction-card-warning">
              <Icon name="calendar" size="md" />
              <div>
                <strong>订阅类购买：对应订阅分组</strong>
                <span>链动小铺购买订阅包时，选择你购买相应的订阅额度分组。</span>
              </div>
            </article>
          </div>

          <div class="instruction-alert instruction-alert-danger">
            <Icon name="exclamationTriangle" size="md" />
            <div>
              <strong>分组选错会导致无法使用。</strong>
              <span>分组决定密钥使用的权益来源，请先判断兑换码来源，再选择对应分组。</span>
            </div>
          </div>

          <div class="instruction-key-flow" aria-label="API 密钥创建步骤">
            <article class="instruction-key-step">
              <div>
                <span>2.1</span>
                <h3>创建密钥</h3>
                <p>进入“API 密钥”页面，点击“创建密钥”。</p>
              </div>
              <figure class="instruction-figure">
                <img src="/img/codex-guide/image-18.png" alt="API 密钥页面暂无密钥并显示创建密钥按钮" loading="lazy" />
                <figcaption>图 4：如果列表为空，直接点击页面中的“创建密钥”。</figcaption>
              </figure>
            </article>
            <article class="instruction-key-step instruction-key-step-focus">
              <div>
                <span>2.2</span>
                <h3>选择分组</h3>
                <p>质保网站补发的兑换码选“质保补偿”；链动小铺额度兑换码选“GPT”或订阅分组。</p>
              </div>
              <figure class="instruction-figure instruction-figure-tall">
                <img src="/img/codex-guide/image-19.png" alt="创建密钥弹窗中选择 API 分组" loading="lazy" />
                <figcaption>图 5：分组决定密钥使用的权益来源，选错会影响后续可用额度。</figcaption>
              </figure>
            </article>
            <article class="instruction-key-step">
              <div>
                <span>2.3</span>
                <h3>使用密钥</h3>
                <p>创建后回到密钥列表，点击“使用密钥”。</p>
              </div>
              <figure class="instruction-figure">
                <img src="/img/codex-guide/image-20.png" alt="密钥列表使用密钥入口" loading="lazy" />
                <figcaption>图 6：进入弹窗后，复制自己的 Codex 配置内容。</figcaption>
              </figure>
            </article>
          </div>

          <h2 id="configPreview">2.2 一键查看接入配置，为后续配置做准备</h2>
          <p>
            密钥创建成功后，在密钥列表的操作列点击“使用密钥”，会弹出接入配置。
            参考页中会直接给出 Codex CLI、Open Code、Claude Code 等客户端的现成配置；后续手动配置以弹窗内容为准。
          </p>
          <section class="instruction-callout">
            <p>
              <strong>重点提示：</strong>
              Codex VSCode 插件、Codex APP 与 Codex CLI 配置完全相同，通常只填一次。
              弹窗里的配置已经把 <code>base_url</code> 和 <code>api_key</code> 填好，优先复制弹窗，不要手动拼错。
            </p>
          </section>
          <figure class="instruction-figure instruction-config-result">
            <img src="/img/codex-guide/image-5.png" alt="使用 API 密钥弹窗中的 Codex 配置示例，密钥已脱敏" loading="lazy" />
            <figcaption>图 7：不要复制教程截图中的示例密钥，请使用你自己页面中生成的 API Key。</figcaption>
          </figure>

          <hr />

          <h1 id="chapterClient">第三章 Codex 客户端接入</h1>
          <section class="instruction-callout">
            <p>
              <strong>说明：</strong>
              本章使用手动修改 <code>config.toml</code> / <code>auth.json</code> 的方式接入 Codex。
              配置前仍需先完成第二章创建 API Key。
            </p>
          </section>
          <p>适用范围：<strong>Codex CLI、Codex VSCode 插件、Codex APP</strong>，三者共用同一份 <code>.codex</code> 配置。</p>

          <div class="instruction-alert instruction-alert-danger">
            <Icon name="exclamationTriangle" size="md" />
            <div>
              <strong>下载好后必须先打开一次 Codex。</strong>
              <span>先打开 Codex 初始化配置文件，然后再完全关闭 Codex，继续下一步文件配置。</span>
            </div>
          </div>
          <a href="https://openai.com/zh-Hans-CN/codex/" target="_blank" rel="noopener noreferrer" class="instruction-inline-link">
            <Icon name="download" size="sm" />
            https://openai.com/zh-Hans-CN/codex/
          </a>
          <figure class="instruction-figure">
            <img src="/img/codex-guide/image-6.png" alt="OpenAI Codex 下载页面截图" loading="lazy" />
            <figcaption>图 8：点击页面中的下载入口获取 Codex。</figcaption>
          </figure>

          <h2 id="installCodex">3.1 手动配置 Codex 系列</h2>
          <p>
            按第二章“使用密钥”弹窗中的 Codex CLI 接入配置，手动修改
            <code>config.toml</code> / <code>auth.json</code>。
            手动配置适用于 <strong>Codex CLI、Codex VSCode 插件、Codex APP</strong>。
          </p>

          <div class="instruction-alert instruction-alert-danger">
            <Icon name="exclamationTriangle" size="md" />
            <div>
              <strong>配置文件前必须退出登录并完全关闭 Codex。</strong>
              <span>请确保 Codex 进程没有在运行，再编辑 <code>config.toml</code> 和 <code>auth.json</code>，否则配置可能不会生效。</span>
            </div>
          </div>

          <h3 id="configureCodex">Windows</h3>
          <ol class="instruction-steps-list">
            <li>首先要保证 Codex 已经下载好，配置文件前必须退出登录并完全关闭 Codex。</li>
            <li>然后在 C 盘找到用户文件夹，在显示中点击显示隐藏文件。</li>
            <li>在用户文件夹打开某一用户文件夹，寻找 <code>.codex</code> 文件夹；如果没有找到，就换一个用户文件夹。</li>
            <li>
              打开 <code>.codex</code> 文件夹之后，如果有 <code>config.toml</code> 和 <code>auth.json</code> 这两个配置文件，直接改动即可；
              如果没有就新建，文件名就是 <code>config.toml</code> 和 <code>auth.json</code>。
            </li>
          </ol>
          <p>如果是新手，直接按下面图片教程替换这两个文件就行了。</p>
          <figure class="instruction-figure">
            <img src="/img/codex-guide/image-31.png" alt="Codex 配置内容粘贴示例，密钥已脱敏" loading="lazy" />
            <figcaption>图 9：配置示例，截图中的 API Key 已脱敏。请使用你自己的密钥，不要复制教程截图。</figcaption>
          </figure>

          <h3 id="configureCodexMac">Mac</h3>
          <ol class="instruction-steps-list">
            <li>在磁盘用户目录中找到 <code>.codex</code> 文件夹，如果找不到就按 <kbd>Command</kbd> + <kbd>Shift</kbd> + <kbd>.</kbd> 显示隐藏文件。</li>
            <li>确认存在 <code>config.toml</code> 和 <code>auth.json</code>，如果没有就新建。文件名就是 <code>config.toml</code> 和 <code>auth.json</code>。</li>
          </ol>
          <div class="instruction-image-grid">
            <figure class="instruction-figure">
              <img src="/img/codex-guide/image-7.png" alt="Mac 访达中找到 .codex 文件夹" loading="lazy" />
              <figcaption>图 10：Mac 在用户目录中找到 <code>.codex</code>。</figcaption>
            </figure>
            <figure class="instruction-figure">
              <img src="/img/codex-guide/image-8.png" alt=".codex 文件夹中的 config.toml 和 auth.json" loading="lazy" />
              <figcaption>图 11：确认存在 <code>config.toml</code> 和 <code>auth.json</code>。</figcaption>
            </figure>
          </div>
          <p>如果是新手，直接按下面图片教程替换这两个文件就行了。</p>
          <figure class="instruction-figure">
            <img src="/img/codex-guide/image-31.png" alt="Codex 配置内容粘贴示例，密钥已脱敏" loading="lazy" />
            <figcaption>图 12：配置示例，截图中的 API Key 已脱敏。请使用你自己的密钥，不要复制教程截图。</figcaption>
          </figure>

          <h2 id="otherClientGuides">3.2 其他客户端配置提醒</h2>
          <p>
            Claude Code、Open Code、Open Claw 和移动端配置都以第二章“使用密钥”弹窗里的真实
            <code>base_url</code> 和 <code>api_key</code> 为准。不同客户端的字段名不同，但核心都是填写中转地址和自己的 API Key。
          </p>
          <div class="instruction-client-grid" aria-label="其他客户端配置入口">
            <article>
              <Icon name="terminal" size="lg" />
              <strong>Claude Code</strong>
              <span>通常配置 <code>ANTHROPIC_BASE_URL</code> 和 <code>ANTHROPIC_AUTH_TOKEN</code>。</span>
            </article>
            <article>
              <Icon name="cube" size="lg" />
              <strong>Open Code</strong>
              <span>通常在 <code>opencode.json</code> 中填写 OpenAI-compatible provider。</span>
            </article>
            <article>
              <Icon name="cloud" size="lg" />
              <strong>Open Claw</strong>
              <span>通常使用 <code>{{ modelsUrl }}</code> 所在的 <code>/v1</code> OpenAI-compatible 地址。</span>
            </article>
            <article>
              <Icon name="chat" size="lg" />
              <strong>移动端</strong>
              <span>Chatbox 等移动端客户端可选择 OpenAI response API 兼容模式。</span>
            </article>
          </div>

          <h2 id="loginCodex">3.3 重新打开 Codex 并使用 API 登录</h2>
          <p>
            完成文件配置后重新打开 Codex，选择“换种方式登录”，再选择 API 登录并粘贴自己的 API 密钥。
            API 密钥从 <a :href="keysUrl" target="_blank" rel="noopener noreferrer">{{ keysUrl }}</a> 获取。
          </p>
          <div class="instruction-image-grid instruction-image-grid-three">
            <figure class="instruction-figure">
              <img src="/img/codex-guide/image-10.png" alt="Codex 选择换种方式登录" loading="lazy" />
              <figcaption>图 13：选择“换种方式登录”。</figcaption>
            </figure>
            <figure class="instruction-figure">
              <img src="/img/codex-guide/image-11.png" alt="Codex API 登录输入框" loading="lazy" />
              <figcaption>图 14：选择 API 登录并粘贴密钥。</figcaption>
            </figure>
            <figure class="instruction-figure">
              <img src="/img/codex-guide/image-12.png" alt="中转服务 API 密钥复制位置，密钥已脱敏" loading="lazy" />
              <figcaption>图 15：从中转后台复制你自己的 API Key。</figcaption>
            </figure>
          </div>

          <hr />

          <h1 id="chapterTrouble">第四章 验证与排错</h1>
          <h2 id="quickCheck">4.1 一行命令自检（推荐）</h2>
          <p>复制下方命令到终端，把 <code>sk-xxxx</code> 换成你的真实密钥。如果能返回模型清单，说明 Key 与 base_url 基本正常。</p>
          <pre class="instruction-code-block"><code>curl {{ modelsUrl }} \
  -H "Authorization: Bearer sk-xxxx"</code></pre>
          <ul class="instruction-steps-list">
            <li><strong>Windows PowerShell</strong> 用户请把 <code>\</code> 续行符换成反引号 <code>`</code>，或直接写成单行。</li>
            <li>如果你的“使用密钥”弹窗显示的 base_url 不是 <code>/v1</code> 结尾，请以弹窗为准调整命令。</li>
          </ul>

          <h2 id="quickChecklist">4.2 登录失败时快速检查</h2>
          <ul class="instruction-checklist">
            <li><Icon name="checkCircle" size="sm" /><span>编辑配置前是否已经完全关闭 Codex？</span></li>
            <li><Icon name="checkCircle" size="sm" /><span><code>config.toml</code> 和 <code>auth.json</code> 是否放在同一个 <code>.codex</code> 目录？</span></li>
            <li><Icon name="checkCircle" size="sm" /><span>是否粘贴了你自己生成的 API Key，而不是教程截图中的示例？</span></li>
            <li><Icon name="checkCircle" size="sm" /><span>创建密钥时是否按来源选择正确分组：质保补发码选“质保补偿”，链动小铺额度兑换码选“GPT”或订阅分组？</span></li>
          </ul>

          <h2 id="troubleTable">4.3 常见报错对照表</h2>
          <div class="instruction-table-wrap">
            <table class="instruction-table">
              <thead>
                <tr>
                  <th>报错 / 现象</th>
                  <th>原因</th>
                  <th>处理方式</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td><code>401 Unauthorized</code> / Incorrect API key</td>
                  <td>密钥错、被删，或配置时 Codex 已经在运行。</td>
                  <td>关闭 Codex，回第二章重新创建或复制密钥，再重新配置 <code>config.toml</code> 并登录。</td>
                </tr>
                <tr>
                  <td><code>404 Not Found</code></td>
                  <td><code>base_url</code> 写错，或客户端需要 <code>/v1</code> 但未填写。</td>
                  <td>检查是否与“使用密钥”弹窗一致；OpenAI-compatible 客户端通常使用 <code>{{ apiV1Url }}</code>。</td>
                </tr>
                <tr>
                  <td><code>余额不足</code> / <code>quota exceeded</code> / <code>429 Too Many Requests</code></td>
                  <td>充值未到账、额度用完、订阅日额度耗尽或触发频率限制。</td>
                  <td>
                    <a :href="profileUrl" target="_blank" rel="noopener noreferrer">打开额度查询页面</a>
                    查看余额和额度；必要时等待刷新或补充额度。
                  </td>
                </tr>
                <tr>
                  <td><code>model not found</code></td>
                  <td>模型 ID 拼错，或当前分组不支持该模型。</td>
                  <td>用 4.1 的 curl 命令查看模型清单，或按中转后台可用模型重新填写。</td>
                </tr>
                <tr>
                  <td>客户端启动后无反应</td>
                  <td>环境变量未生效，旧终端还在使用旧配置。</td>
                  <td>关闭并新开一个终端窗口，再启动 <code>codex</code> / <code>claude</code> / <code>opencode</code>。</td>
                </tr>
                <tr>
                  <td><code>config.toml.txt</code> / <code>opencode.json.txt</code></td>
                  <td>Windows 默认隐藏文件后缀，实际创建成了文本文件。</td>
                  <td>资源管理器 → 查看 → 勾选“文件扩展名”，再把文件名改正确。</td>
                </tr>
                <tr>
                  <td>原 Codex 聊天记录不见</td>
                  <td>切换 API 中转后，本地 provider 不一致。</td>
                  <td>
                    参考
                    <a href="https://github.com/Dailin521/codex-provider-sync/releases" target="_blank" rel="noopener noreferrer">
                      codex-provider-sync releases
                    </a>
                    恢复。
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
          <figure class="instruction-figure instruction-error-figure">
            <img src="/img/codex-guide/image-14.png" alt="Codex 登录时报 401 Incorrect API key，密钥已脱敏" loading="lazy" />
            <figcaption>图 16：错误示例，API Key 片段已脱敏。</figcaption>
          </figure>

          <h1 id="faq">第五章 FAQ</h1>
          <div class="instruction-faq-list">
            <p><strong>Q1：一个账号能创建几把密钥？</strong><br />可创建多把，建议按客户端 / 设备分别命名，便于审计和单独吊销。</p>
            <p><strong>Q2：泄露密钥怎么办？</strong><br />立即在“API 密钥”页面删除原密钥，重新创建一把，然后更新所有客户端的配置。</p>
            <p><strong>Q3：Codex / Claude Code / Open Code 可以共用一把密钥吗？</strong><br />可以，但不建议。多把密钥独立计费、独立吊销，出问题时排查更快。</p>
            <p><strong>Q4：充值的钱和订阅额度怎么消费？</strong><br />额度模式按调用量从余额扣款；订阅模式则在订阅周期或每日额度内使用，具体计费规则以中转后台实时显示为准。</p>
            <p><strong>Q5：技术支持怎么联系？</strong><br />可查看页面上方交流群二维码，或登录中转站后在个人中心、站内公告、客服入口查看最新联系方式。</p>
          </div>
        </article>
      </main>
    </div>
  </div>
</template>

<script setup lang="ts">
import Icon from '@/components/icons/Icon.vue'

const siteUrl = 'https://aichatgpt.cc.cd'
const baseUrl = `${siteUrl}/`
const apiV1Url = `${siteUrl}/v1`
const modelsUrl = `${apiV1Url}/models`
const registerUrl = `${siteUrl}/register`
const profileUrl = `${siteUrl}/profile`
const redeemUrl = `${siteUrl}/redeem`
const keysUrl = `${siteUrl}/keys`
</script>

<style scoped>
.instruction-page {
  --doc-bg: #f7faf9;
  --doc-surface: #ffffff;
  --doc-line: #dfe7e4;
  --doc-line-strong: #b8d2cb;
  --doc-text: #16252b;
  --doc-muted: #5f7177;
  --doc-accent: #0f9f85;
  --doc-accent-soft: #e9f8f4;
  min-height: 100vh;
  padding: 0 1rem 3rem;
  color: var(--doc-text);
  background: var(--doc-bg);
}

.instruction-header {
  position: sticky;
  top: 0;
  z-index: 50;
  margin: 0 -1rem;
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--doc-line);
  background: rgba(255, 255, 255, 0.93);
  backdrop-filter: blur(14px);
}

.instruction-nav {
  display: flex;
  width: min(100%, 1280px);
  margin: 0 auto;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.instruction-brand,
.instruction-actions,
.instruction-link,
.instruction-primary-link,
.instruction-inline-link,
.instruction-badges span {
  display: inline-flex;
  align-items: center;
}

.instruction-brand {
  min-width: 0;
  gap: 0.75rem;
  color: var(--doc-text);
  text-decoration: none;
}

.instruction-brand img {
  width: 42px;
  height: 42px;
  border-radius: 8px;
  box-shadow: 0 8px 20px rgba(15, 159, 133, 0.18);
}

.instruction-brand strong,
.instruction-brand small {
  display: block;
}

.instruction-brand strong {
  font-size: 1rem;
  font-weight: 900;
}

.instruction-brand small {
  margin-top: 0.1rem;
  color: var(--doc-muted);
  font-size: 0.82rem;
}

.instruction-actions {
  justify-content: flex-end;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.instruction-link,
.instruction-primary-link,
.instruction-inline-link {
  gap: 0.45rem;
  min-height: 40px;
  padding: 0.6rem 0.85rem;
  border-radius: 8px;
  font-weight: 800;
  text-decoration: none;
  transition: 0.18s ease;
}

.instruction-link {
  border: 1px solid var(--doc-line);
  background: #fff;
  color: var(--doc-muted);
}

.instruction-primary-link,
.instruction-inline-link {
  border: 1px solid rgba(15, 159, 133, 0.25);
  background: var(--doc-accent);
  color: #fff;
}

.instruction-inline-link {
  width: fit-content;
  max-width: 100%;
  overflow-wrap: anywhere;
}

.instruction-link:hover,
.instruction-primary-link:hover,
.instruction-inline-link:hover {
  transform: translateY(-1px);
  border-color: var(--doc-accent);
}

.instruction-frame {
  display: grid;
  width: min(100%, 1480px);
  margin: 0 auto;
  grid-template-columns: 290px minmax(0, 1fr);
  gap: 1.25rem;
  align-items: start;
}

.instruction-toc {
  position: sticky;
  top: 5rem;
  display: grid;
  gap: 1rem;
  max-height: calc(100vh - 6rem);
  overflow: auto;
  overscroll-behavior: contain;
  margin-top: 2rem;
  padding: 1rem;
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 18px 48px rgba(38, 84, 74, 0.12);
  scrollbar-width: thin;
}

.instruction-toc-heading {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr);
  gap: 0.75rem;
  align-items: center;
}

.instruction-toc-heading strong,
.instruction-toc-heading span {
  display: block;
}

.instruction-toc-heading strong {
  color: var(--doc-text);
  font-weight: 900;
}

.instruction-toc-heading span {
  margin-top: 0.15rem;
  color: var(--doc-muted);
  font-size: 0.88rem;
}

.instruction-toc nav,
.instruction-toc section {
  display: grid;
  gap: 0.55rem;
}

.instruction-toc nav {
  gap: 0.9rem;
}

.instruction-toc p {
  margin: 0;
  color: var(--doc-text);
  font-size: 0.92rem;
  font-weight: 900;
}

.instruction-toc a {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr);
  gap: 0.5rem;
  align-items: center;
  padding: 0.58rem 0.7rem;
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #fff;
  color: var(--doc-muted);
  text-decoration: none;
  transition: 0.18s ease;
}

.instruction-toc a:hover {
  border-color: var(--doc-accent);
  color: var(--doc-accent);
  transform: translateX(2px);
}

.instruction-shell {
  min-width: 0;
  padding-top: 2rem;
}

.instruction-hero {
  display: grid;
  gap: 1rem;
  padding: clamp(1.35rem, 4vw, 2.5rem);
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 20px 56px rgba(38, 84, 74, 0.12);
}

.instruction-base {
  width: fit-content;
  margin: 0;
  padding: 0.5rem 0.75rem;
  border: 1px solid rgba(15, 159, 133, 0.22);
  border-radius: 8px;
  background: var(--doc-accent-soft);
  color: #0b806d;
  font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
  font-size: 0.9rem;
  font-weight: 800;
}

.instruction-hero h1 {
  max-width: 900px;
  margin: 0;
  color: #10252e;
  font-size: clamp(2rem, 5vw, 3.6rem);
  line-height: 1.04;
}

.instruction-hero > p:not(.instruction-base) {
  max-width: 900px;
  margin: 0;
  color: var(--doc-muted);
  font-size: clamp(1rem, 2.3vw, 1.18rem);
  line-height: 1.8;
}

.instruction-badges,
.instruction-jump,
.instruction-card-grid,
.instruction-two-grid,
.instruction-support-grid,
.instruction-image-grid,
.instruction-key-flow,
.instruction-checklist {
  display: grid;
  gap: 0.85rem;
}

.instruction-badges {
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}

.instruction-badges span {
  gap: 0.45rem;
  padding: 0.75rem 0.9rem;
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #fff;
  color: var(--doc-text);
  font-weight: 850;
}

.instruction-jump {
  grid-template-columns: repeat(4, minmax(0, 1fr));
  margin-top: 0.25rem;
}

.instruction-jump a {
  padding: 0.85rem 1rem;
  border: 1px solid rgba(15, 159, 133, 0.22);
  border-radius: 8px;
  background: var(--doc-accent-soft);
  color: #0b806d;
  font-weight: 900;
  text-align: center;
  text-decoration: none;
}

.instruction-article {
  min-width: 0;
  margin-top: 1.2rem;
  padding: clamp(1.1rem, 3vw, 2.1rem);
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 20px 56px rgba(38, 84, 74, 0.1);
}

.instruction-article h1,
.instruction-article h2,
.instruction-article h3 {
  color: #10252e;
}

.instruction-article h1 {
  margin: 2.3rem 0 1rem;
  font-size: clamp(1.75rem, 4vw, 2.45rem);
  line-height: 1.15;
}

.instruction-article > h1:first-child {
  margin-top: 0;
}

.instruction-article h2 {
  margin: 2rem 0 0.8rem;
  font-size: clamp(1.25rem, 2.6vw, 1.7rem);
}

.instruction-article h3 {
  margin: 1.5rem 0 0.6rem;
  font-size: 1.06rem;
}

.instruction-article p,
.instruction-article li,
.instruction-table,
.instruction-figure figcaption,
.instruction-card span,
.instruction-two-grid span,
.instruction-support-card span,
.instruction-checklist span,
.instruction-client-grid span,
.instruction-key-step p {
  color: var(--doc-muted);
  line-height: 1.78;
}

.instruction-article p {
  margin: 0.65rem 0;
}

.instruction-article a {
  color: #0b806d;
  font-weight: 850;
}

.instruction-article hr {
  margin: 2.2rem 0;
  border: 0;
  border-top: 1px solid var(--doc-line);
}

.instruction-callout,
.instruction-alert,
.instruction-card,
.instruction-two-grid article,
.instruction-support-card,
.instruction-checklist li,
.instruction-key-step,
.instruction-config-result,
.instruction-client-grid article,
.instruction-faq-list p {
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: var(--doc-accent-soft);
}

.instruction-callout {
  margin: 1rem 0;
  padding: 1rem;
}

.instruction-callout-important {
  border-color: rgba(15, 159, 133, 0.32);
  background: #f3fbf8;
}

.instruction-callout p:first-child,
.instruction-callout p:last-child,
.instruction-callout ul:last-child {
  margin-top: 0;
  margin-bottom: 0;
}

.instruction-terms ul {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 0.75rem;
  margin: 0.8rem 0 0;
  padding: 0;
  list-style: none;
}

.instruction-terms li {
  min-width: 0;
  padding: 0.85rem;
  border: 1px solid rgba(15, 159, 133, 0.18);
  border-radius: 8px;
  background: #fff;
}

.instruction-table-wrap {
  width: 100%;
  overflow-x: auto;
  margin: 0.9rem 0;
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #fff;
}

.instruction-table {
  width: 100%;
  min-width: 560px;
  border-collapse: collapse;
  font-size: 0.95rem;
}

.instruction-table th,
.instruction-table td {
  padding: 0.9rem 1rem;
  border-bottom: 1px solid var(--doc-line);
  text-align: left;
  vertical-align: top;
}

.instruction-table th {
  width: 170px;
  color: var(--doc-text);
  background: #f3fbf8;
  font-weight: 950;
}

.instruction-table tr:last-child th,
.instruction-table tr:last-child td {
  border-bottom: 0;
}

.instruction-alert {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr);
  gap: 0.75rem;
  margin: 1rem 0;
  padding: 1rem;
}

.instruction-alert strong,
.instruction-alert span,
.instruction-card strong,
.instruction-card span,
.instruction-two-grid strong,
.instruction-two-grid span,
.instruction-support-card strong,
.instruction-support-card span,
.instruction-client-grid strong,
.instruction-client-grid span {
  display: block;
}

.instruction-alert strong,
.instruction-card strong,
.instruction-two-grid strong,
.instruction-support-card strong,
.instruction-key-step h3,
.instruction-client-grid strong {
  color: var(--doc-text);
}

.instruction-alert-info {
  border-color: rgba(14, 165, 233, 0.24);
  background: #eef9ff;
}

.instruction-alert-danger,
.instruction-card-danger {
  border-color: rgba(244, 63, 94, 0.24);
  background: #fff1f2;
}

.instruction-card-warning {
  border-color: rgba(245, 158, 11, 0.26);
  background: #fffbeb;
}

.instruction-card-success,
.instruction-two-grid article {
  border-color: rgba(15, 159, 133, 0.24);
  background: #ecfdf7;
}

.instruction-card-grid {
  grid-template-columns: repeat(3, minmax(0, 1fr));
  margin: 1rem 0;
}

.instruction-two-grid {
  grid-template-columns: repeat(2, minmax(0, 1fr));
  margin: 0.8rem 0 1rem;
}

.instruction-card,
.instruction-two-grid article {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr);
  gap: 0.75rem;
  align-items: start;
  padding: 1rem;
}

.instruction-support-grid {
  grid-template-columns: minmax(0, 1fr) minmax(180px, 260px);
  align-items: center;
  margin: 1.1rem 0;
}

.instruction-support-card {
  display: grid;
  align-content: start;
  gap: 0.8rem;
  min-height: 0;
  padding: 1.2rem;
  background: #fff;
}

.instruction-figure {
  display: grid;
  gap: 0.55rem;
  margin: 1rem 0;
}

.instruction-figure img {
  display: block;
  width: 100%;
  height: auto;
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 14px 36px rgba(38, 84, 74, 0.12);
}

.instruction-qr {
  align-self: start;
  margin: 0;
}

.instruction-qr img {
  max-height: 220px;
  object-fit: contain;
}

.instruction-image-grid {
  grid-template-columns: repeat(2, minmax(0, 1fr));
  margin: 1rem 0;
}

.instruction-image-grid-three {
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.instruction-key-step {
  display: grid;
  grid-template-columns: minmax(160px, 0.36fr) minmax(0, 1fr);
  gap: 1rem;
  align-items: center;
  padding: 1rem;
  background: #fff;
}

.instruction-key-step-focus,
.instruction-config-result {
  border-color: rgba(15, 159, 133, 0.3);
  background: #f4fffb;
}

.instruction-key-step > div {
  display: grid;
  gap: 0.45rem;
}

.instruction-key-step span:first-child {
  display: inline-flex;
  width: fit-content;
  min-width: 2.5rem;
  align-items: center;
  justify-content: center;
  padding: 0.35rem 0.65rem;
  border-radius: 8px;
  background: var(--doc-accent-soft);
  color: #0b806d;
  font-weight: 950;
}

.instruction-key-step h3,
.instruction-key-step .instruction-figure {
  margin: 0;
}

.instruction-figure-tall img {
  width: min(100%, 420px);
  justify-self: center;
  max-height: 460px;
  object-fit: contain;
}

.instruction-steps-list,
.instruction-checklist {
  margin: 1rem 0;
}

.instruction-steps-list {
  display: grid;
  gap: 0.55rem;
  padding-left: 1.3rem;
}

.instruction-checklist {
  padding: 0;
  list-style: none;
}

.instruction-checklist li {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr);
  gap: 0.65rem;
  align-items: start;
  padding: 0.9rem 1rem;
  background: #fff;
}

.instruction-client-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 0.85rem;
  margin: 1rem 0;
}

.instruction-client-grid article {
  display: grid;
  gap: 0.55rem;
  padding: 1rem;
  background: #fff;
}

.instruction-card-success svg,
.instruction-two-grid svg,
.instruction-checklist svg,
.instruction-badges svg,
.instruction-client-grid svg {
  color: #0b806d;
}

.instruction-card-warning svg {
  color: #b45309;
}

.instruction-card-danger svg,
.instruction-alert-danger svg {
  color: #e11d48;
}

.instruction-page code,
.instruction-page kbd {
  border: 1px solid var(--doc-line-strong);
  border-radius: 6px;
  background: #f3fbf8;
  color: #0f3f37;
  font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
  font-size: 0.88em;
}

.instruction-page code {
  padding: 0.12rem 0.35rem;
}

.instruction-page kbd {
  padding: 0.08rem 0.34rem;
}

.instruction-code-block {
  width: 100%;
  overflow-x: auto;
  margin: 1rem 0;
  padding: 1rem;
  border: 1px solid var(--doc-line);
  border-radius: 8px;
  background: #07131b;
  color: #d9fff3;
  box-shadow: 0 14px 36px rgba(7, 19, 27, 0.16);
}

.instruction-code-block code {
  display: block;
  min-width: max-content;
  padding: 0;
  border: 0;
  background: transparent;
  color: inherit;
  font-size: 0.9rem;
  line-height: 1.7;
  white-space: pre;
}

.instruction-faq-list {
  display: grid;
  gap: 0.8rem;
}

.instruction-faq-list p {
  margin: 0;
  padding: 1rem;
  background: #fff;
}

.instruction-error-figure img {
  max-height: 520px;
  object-fit: contain;
}

@media (max-width: 1100px) {
  .instruction-frame {
    grid-template-columns: 1fr;
  }

  .instruction-toc {
    position: static;
    max-height: none;
    overflow: visible;
  }
}

@media (max-width: 820px) {
  .instruction-page {
    padding-inline: 0.75rem;
  }

  .instruction-header {
    margin-inline: -0.75rem;
    padding: 0.5rem 0.75rem;
  }

  .instruction-brand {
    flex: 1 1 auto;
    gap: 0.5rem;
  }

  .instruction-brand img {
    width: 34px;
    height: 34px;
  }

  .instruction-brand strong {
    font-size: 0.9rem;
    white-space: nowrap;
  }

  .instruction-brand small {
    display: none;
  }

  .instruction-actions {
    flex: 0 0 auto;
    gap: 0.35rem;
    width: auto;
  }

  .instruction-link,
  .instruction-primary-link {
    width: auto;
    min-height: 34px;
    padding: 0.45rem 0.55rem;
    font-size: 0.8rem;
    white-space: nowrap;
  }

  .instruction-jump,
  .instruction-card-grid,
  .instruction-two-grid,
  .instruction-support-grid,
  .instruction-image-grid,
  .instruction-image-grid-three,
  .instruction-key-step,
  .instruction-client-grid,
  .instruction-terms ul {
    grid-template-columns: 1fr;
  }

  .instruction-table {
    min-width: 520px;
  }
}

@media (max-width: 520px) {
  .instruction-shell {
    padding-top: 1rem;
  }

  .instruction-hero,
  .instruction-article {
    border-radius: 8px;
  }

  .instruction-badges {
    grid-template-columns: 1fr;
  }

  .instruction-brand img {
    width: 32px;
    height: 32px;
  }

  .instruction-brand strong {
    font-size: 0.86rem;
  }

  .instruction-actions {
    gap: 0.3rem;
  }

  .instruction-link,
  .instruction-primary-link {
    min-height: 32px;
    padding: 0.4rem 0.5rem;
    font-size: 0.78rem;
  }
}
</style>
