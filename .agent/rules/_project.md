---
trigger: always_on
---

This file provides guidance for `AI Agent` working on the taro4-template project. taro4-template is a mini-program development template project based on Taro, focused on multi-platform mini-program development for WeChat, Alipay, and others, without involving native apps.

## [STEP-0] Core Constraints

- **Platform**: Only supports mini-program platforms, NEVER add React Native or native app configurations
- **Tech Stack**: Taro 4.x + React/Vue + TypeScript + SCSS
- **API**: Use Taro API uniformly, NEVER directly call wx/my or other platform-specific APIs
- **Components**: Use View/Text/Image, NEVER use button/div/span or other HTML tags
- **Styling**: Use rpx units and Flexbox layout, avoid Grid and px
- **Routing**: Use useRouter from @tarojs/taro, NEVER use react-router-dom

## [STEP-1] Standard Structure

- [src/](/src/): Source code (app.ts, pages/, components/, utils/, api/, store/)
- [config/](/config/): Build configuration (index.ts, dev.ts, prod.ts)
- [project.config.json](/project.config.json): WeChat mini-program configuration
- [package.json](/package.json): Project dependencies

## [STEP-2] Development Standards

### [STEP-2.1] Styling Standards

````xml
<examples xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="/_ai/meta/example.xsd">
  <good-example description="Using rpx units and Flexbox layout">
    ```scss
    .product-card {
      display: flex;
      flex-direction: column;
      padding: 20rpx;

      &__title {
        font-size: 32rpx;
        color: #333;
      }
    }
    ```
    <summary>
      Correctly using rpx units ensures multi-screen adaptation, using Flexbox layout ensures compatibility.
    </summary>
  </good-example>

  <bad-example description="Using px units or Grid layout">
    ```scss
    .product-card {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      padding: 20px;
    }
    ```
    <summary>
      MUST NOT use px units (non-responsive) and Grid layout (compatibility issues).
    </summary>
  </bad-example>
</examples>
````

### [STEP-2.2] TypeScript and Error Handling

````xml
<examples xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="/_ai/meta/example.xsd">
  <good-example description="Using TypeScript types and error handling">
    ```typescript
    interface Product {
      id: string
      name: string
      price: number
    }

    async function fetchProduct(id: string): Promise<Product | null> {
      try {
        const res = await Taro.request<{ data: Product }>({
          url: `https://api.example.com/products/${id}`
        })
        return res.data.data
      } catch (error) {
        Taro.showToast({ title: '加载失败', icon: 'none' })
        return null
      }
    }
    ```
    <summary>
      Defines clear TypeScript interfaces with complete error handling.
    </summary>
  </good-example>

  <bad-example description="Using any type and missing error handling">
    ```typescript
    async function fetchProduct(id: any) {
      const res = await Taro.request({ url: `/products/${id}` })
      return res.data
    }
    ```
    <summary>
      Using any loses type safety, missing error handling can cause application crashes.
    </summary>
  </bad-example>
</examples>
````

### [STEP-2.3] Performance Optimization

- **Subpackaging**: Use subpackages and preloadRule to reduce main package size
- **Caching**: Use Taro.setStorage to cache data with reasonable expiration times
- **Images**: Use mode="widthFix" or "aspectFill" to control image rendering
- **Long Lists**: Use VirtualList to optimize scrolling performance

## [STEP-3] AI Agent Responsibility Boundaries

### [STEP-3.1] Proactive Execution Allowed

- Optimize build configuration and compilation performance
- Improve code structure and maintainability
- Supplement missing TypeScript type definitions
- Add missing exception handling and user prompts

### [STEP-3.2] Execution Prohibited

- Add React Native or H5 related configurations
- Switch from React to Vue or vice versa
- Upgrade Taro or other core dependencies to major versions
- Modify core business logic or API interfaces

### [STEP-3.3] Verification Process

After completing code modifications, MUST execute the following verifications:

```bash
npm run type-check
npm run lint
npm run build:weapp
```

## [STEP-4] Coordination with Knowledge Base

The taro4-template project has corresponding knowledge base documentation in the TrueNine_Life repository:

- Knowledge card: frameworks/Taro.md
- Project prompts: _airef/taro4-template/
- Ensure template updates are reflected in knowledge base documentation

````xml
<examples xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="/_ai/meta/example.xsd">
  <good-example description="Synchronizing knowledge base after template update">
    <thinking>
      Updated taro4-template to Taro 4.x.
      Should also update frameworks/Taro.md knowledge card with version info.
    </thinking>
    <tooling name="Update" params:path="C:\Users\<name>\project\taro4-template\package.json" />
    <tooling name="Update" params:path="frameworks\Taro.md" />
    <summary>
      Upgraded template Taro version and synchronized updates to knowledge base card.
    </summary>
  </good-example>
</examples>
````
