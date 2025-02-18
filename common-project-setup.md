
  # 1. Project Setup

### 1.1 Dynamic Entry Point Configuration

Enable a dynamic entry point for your project, by following these steps to modify the `index.html` file appropriately.

####  Modify `index.html`

1. **Navigate to** the root directory of your project and locate the `index.html` file.
2. **Update the script reference** inside the `<body>` tag by replacing the hardcoded script source with a dynamic placeholder.

3. **Before Modification**:
The default `index.html` contains a static script reference pointing to `main.tsx`:

```html
<!-- index.html -->
<body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script> <!-- ✅ Change pending implementation. -->
</body>
```

4. **After Modification**:
Replace the static script tag with the dynamic template placeholder `<%- injectMainScript %>:`

```html
<!-- index.html -->
<body>
    <div id="root"></div>
    <%- injectMainScript %> <!-- ✅ Change Made -->
</body>
```

### 1.2 Modify Vite Config File:

1. **Navigate to** the root directory of your project and locate the `vite.config.ts` file.
2. **Update** the **plugin** in `defineConfig` with the following code.

    **Before Modification**:
    Add this import:
    
    ```ts
    import { createHtmlPlugin } from 'vite-plugin-html';
    ```
    
    Then, update the `plugins` array:
    
    ```ts
    plugins: [react(), tsConfigPaths(), eslint({ fix: true })],
    ```

    **After Modification**:

    ```ts
    // vite.config.ts
    import { createHtmlPlugin } from 'vite-plugin-html';

    plugins: [
        react(),
        tsConfigPaths(),
        eslint({ fix: true }),
        createHtmlPlugin({
            inject: {
                data: {
                    injectMainScript: '<script type="module" src="./src/main.tsx"></script>',
                },
            },
            minify: true,
        }),
    ],
    ```

### 1.3 Create Vite Config File for Mobile App:

1. First, navigate to your project's root directory and create a new file called `vitemob.config.ts`.
2. From there, locate the existing `vite.config.ts` file in the same directory and duplicate its entire codebase into your newly created `vitemob.config.ts` file apply the following modifications.

    **vite.config.ts file**:

    ```ts
    // vite.config.ts
    plugins: [
        react(),
        tsConfigPaths(),
        eslint({ fix: true }),
        createHtmlPlugin({
            inject: {
                data: {
                    injectMainScript: '<script type="module" src="./src/main.tsx"></script>', // ✅ Replace this line 
                },
            },
            minify: true,
        }),
    ],
    ```

    **New vitemob.config.ts file**:

    ```ts
    // vitemob.config.ts
    plugins: [
        react(),
        tsConfigPaths(),
        eslint({ fix: true }),
        createHtmlPlugin({
            inject: {
                data: {
                    injectMainScript: '<script type="module" src="./src/mobMain.tsx"></script>', // ✅ Changes Made
                },
            },
            minify: true,
        }),
    ],
    ```


### 1.4 Create MobileAppProvide component:
1. First, navigate to your project's provider directory at src => packages => core => providers and create a new file called `MobileAppProvider.tsx`.

2. From there, locate the existing `app.tsx` file in the same directory and duplicate its entire codebase into your newly created `MobileAppProvider.tsx file`.

3. Within` MobileAppProvider.tsx`, you'll need to update the component naming convention - specifically, replace all instances of `AppProvider` with `MobileAppProvider` and `AppProviderProps` with `MobileAppProviderProps` to reflect its mobile-specific purpose.

4. Finally, integrate the new `MobileAppProvider` component by modifying the `AppCoreProvider.tsx` file according to the code snippets below:

    **Before Modification**:

    ```tsx
    // AppCoreProvider.tsx
    import BrowserOffline from '@/components/Custom/BrowserOffline';
    import Spinner from '@core/components/Elements/Spinner';
    import AppProvider from '@core/providers/app';
    import { actions } from '@core/store';
    import { Config } from '@core/types';
    import { RouterProvider } from 'react-router-dom';

    export const AppCoreProvider: React.FC<{ config: Config }> = ({ config }) => {
    actions.config.initialize(config);

    return (
        <AppProvider>
        <BrowserOffline />
        <RouterProvider router={config.router} fallbackElement={<Spinner />} />
        </AppProvider>
    );
    };
    ```

    **After Modification**:

    ```tsx 
    // AppCoreProvider.tsx
    import BrowserOffline from '@/components/Custom/BrowserOffline';
    import Spinner from '@core/components/Elements/Spinner';
    import AppProvider from '@core/providers/app';
    import { actions } from '@core/store';
    import { Config } from '@core/types';
    import { RouterProvider } from 'react-router-dom';
    import MobileAppProvider from './MobileAppProvider'; // ✅ New Line of code

    export const AppCoreProvider: React.FC<{ config: Config }> = ({ config }) => {
    actions.config.initialize(config);

    return (
        <AppProvider>
        <BrowserOffline />
        <RouterProvider router={config.router} fallbackElement={<Spinner />} />
        </AppProvider>
    );
    };

    // ✅ New block of code
    export const MobileAppCoreProvider: React.FC<{ config: Config }> = ({ config }) => {
    actions.config.initialize(config);

    return (
        <MobileAppProvider>
        <BrowserOffline />
        <RouterProvider router={config.router} fallbackElement={<Spinner />} />
        </MobileAppProvider>
    );
    };
    // ✅ New block of code
    ```

### 1.5 Create MobileApp component:

1. First, navigate to your project's `src` directory and create a new file called `MobileApp.tsx`.
2. From there, locate the existing `App.tsx` file in the same directory and duplicate its entire codebase into your newly created `MobileApp.tsx` file.
3. Within `MobileApp.tsx`, you'll need to update the component naming convention - specifically, replace all instances of `App` with `MobileApp` and import `MobileAppCoreProvider` component and use this component in place of `AppCoreProvider`.

    **App.tsx file**:

    ```tsx
    //App.tsx file
    import { AppCoreProvider } from '@core/providers';
    import { Config } from '@core/types';
    import { publicRoutes } from '@/routes/public';

    function App() {
    const config: Config = {
        apiUrl: import.meta.env.VITE_API_URL,
        wsUrl: import.meta.env.VITE_WS_URL,
        environment: import.meta.env.MODE,
        storageKeyPrefix: 'tzm-palm_',
        projectName: 'Palm Meadows',
        defaultRoute: '/app/home',
        router: publicRoutes,
    };
    return <AppCoreProvider config={config} />;
    }

    export default App;
    ```

    **New MobileApp.tsx file**:

    ```tsx
    // MobileApp.tsx file
    import { MobileAppCoreProvider } from '@core/providers/AppCoreProvider'; // ✅ Changes Made
    import { Config } from '@core/types';
    import { publicRoutes } from '@/routes/public';

    function MobileApp() {      // ✅ Changes Made
    const config: Config = {
        apiUrl: import.meta.env.VITE_API_URL,
        wsUrl: import.meta.env.VITE_WS_URL,
        environment: import.meta.env.MODE,
        storageKeyPrefix: 'tzm-palm_',
        projectName: 'Palm Meadows',
        defaultRoute: '/app/home',
        router: publicRoutes,
    };
    return <MobileAppCoreProvider config={config} />; // ✅ Changes Made
    }

    export default MobileApp; // ✅ Changes Made

    ```


### 1.6 Create mobMain component:

1. First, navigate to your project's `src` directory and create a new file called `mobMain.tsx`.
2. From there, locate the existing `main.tsx` file in the same directory and duplicate its entire codebase into your newly created `mobMain.tsx` file.
3. Within `mobMain.tsx`, made the following changes.

    **main.tsx file**:
    ```tsx 
    // main.tsx 
    import '@core/utils/wdyr';
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import 'leaflet/dist/leaflet.css';
    import './index.css';
    import { ApolloProvider } from '@apollo/client';
    import client from '@core/lib/apolloClient/apolloClient';

    const App = React.lazy(() => import('./App')); // ✅ Change pending implementation.

    ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
    <React.StrictMode>
        <ApolloProvider client={client}>
        <App />  // ✅ Change pending implementation.
        </ApolloProvider>
    </React.StrictMode>

    );
    ```

    **New mobMain.tsx file**:

    ```tsx 
    // mobMain.tsx 
    import '@core/utils/wdyr';
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import 'leaflet/dist/leaflet.css';
    import './index.css';
    import { ApolloProvider } from '@apollo/client';
    import client from '@core/lib/apolloClient/apolloClient';

    const MobileApp = React.lazy(() => import('./MobileApp'));  // ✅ Changes Made

    ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
    <React.StrictMode>
        <ApolloProvider client={client}>
        <MobileApp />  // ✅ Changes Made
        </ApolloProvider>
    </React.StrictMode>
    );
    ```

    