# 源组件和依赖

与 *Build Type* 类似，*Product Flavor* 也会通过它们自己的 *sourceSet* 提供代码和资源。

之前的例子将会创建 4 个 *sourceSet*：

* **<font color='green'>android.sourceSets.flavor1</font>**
位于 `src/flavor1/`
* **<font color='green'>android.sourceSets.flavor2</font>**
位于 `src/flavor2/`
* **<font color='green'>android.sourceSets.androidTestFlavor1</font>**
位于 `src/androidTestFlavor1/`
* **<font color='green'>android.sourceSets.androidTestFlavor2</font>**
位于 `src/androidTestFlavor2/`

这些 *sourceSet* 用于与 **<font color='green'>android.sourceSets.main</font>** 和 *Build Type* 的 *sourceSet* 来构建 APK。下面的规则用于处理所有 sourceSet 来构建 APK：

* 多个文件夹中的所有的源代码（`src/*/java`）都会合并起来生成一个输出。
* 所有的 Manifest 文件都会合并成一个 Manifest 文件。类似于 *Build Type*，允许 *Product Flavor* 可以拥有不同的的组件和权限声明。
* 所有资源（Android res 和 assets）遵循的优先级为 *Build Type* 覆盖 *Product Flavor*，最终覆盖 **<font color='green'>main</font>** *sourceSet* 的资源。
* 每个 *Build Variant* 都会根据资源生成自己的 R 类（或者其它一些源代码）。Variant 之间互相独立。

最终，类似 *Build Type*，*Product Flavor* 也可以有它们的依赖关系。例如，如果使用 flavor 来生成一个基于广告的应用版本和一个付费的应用版本，其中广告版本可能需要依赖于广告 SDK，但是付费版不需要。

``` Groovy
dependencies {
    flavor1Compile "..."
}
```

在这个例子中，`src/flavor1/AndroidManifest.xml` 文件中可能需要声明访问网络的权限。

每一个 Variant 也会创建额外的 sourceSet：

* **<font color='green'>android.sourceSets.flavor1Debug</font>**
位于 `src/flavor1Debug/`
* **<font color='green'>android.sourceSets.flavor1Release</font>**
位于 `src/flavor1Release/`
* **<font color='green'>android.sourceSets.flavor2Debug</font>**
位于 `src/flavor2Debug/`
* **<font color='green'>android.sourceSets.flavor2Release</font>**
位于 `src/flavor2Release/`

这些 sourceSet 拥有比 Build Type 的 sourceSet 更高的优先级，并允许在 Variant 的层次上做一些定制。