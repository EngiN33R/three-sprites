[**three-sprites**](../index.md) • **Docs**

***

# Class: TilemapMeshPhongMaterial

THREE.MeshPhongMaterial extending TilemapMaterial.

```
const material = new THREE.TilemapMeshPhongMaterial({
  map: myTexture,
});

materiial.tile({
  tiles: [1, 2, 3, 4, 5, 6, 7],
  tileSize: { x: 16, y: 16 },
  tilesetSize: { x: 128, y: 128 },
});
```

## Extends

- [`TilemapMaterial`](TilemapMaterial.md)\<`this`\> & *typeof* `MeshPhongMaterial`

## Constructors

### new TilemapMeshPhongMaterial()

> **new TilemapMeshPhongMaterial**(): [`TilemapMeshPhongMaterial`](TilemapMeshPhongMaterial.md)

#### Returns

[`TilemapMeshPhongMaterial`](TilemapMeshPhongMaterial.md)

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).constructor`

#### Defined in

src/TilemapMaterial.ts:357

***

### new TilemapMeshPhongMaterial()

> **new TilemapMeshPhongMaterial**(`parameters`?): `MeshPhongMaterial`

#### Parameters

| Parameter | Type |
| ------ | ------ |
| `parameters`? | `MeshPhongMaterialParameters` |

#### Returns

`MeshPhongMaterial`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).constructor`

#### Defined in

src/index.ts:199

## Properties

| Property | Modifier | Type | Description | Inherited from | Defined in |
| ------ | ------ | ------ | ------ | ------ | ------ |
| `map?` | `public` | `null` \| `Texture` | The texture for the Tilemap. https://threejs.org/docs/?q=basicmat#api/en/materials/MeshBasicMaterial.map | `TilemapMaterial.extendClass(THREE.MeshPhongMaterial).map` | src/TilemapMaterial.ts:124 |
| `prototype` | `public` | `MeshPhongMaterial` | - | `TilemapMaterial.extendClass(THREE.MeshPhongMaterial).prototype` |  |
| `tiling?` | `public` | `Required`\<[`ITilemapTilingOptions`](../interfaces/ITilemapTilingOptions.md)\<`Vector2`\>\> | The tiling options set via `.tile()`. Manipulating them directly takes no effect until `.tile()` is called again. | `TilemapMaterial.extendClass(THREE.MeshPhongMaterial).tiling` | src/TilemapMaterial.ts:146 |
| `uniforms?` | `public` | [`ITilemapUniforms`](../interfaces/ITilemapUniforms.md) | Uniforms of the shader. May be set before shader compilation. `const mat = new SpriteMaterial({ map: myTexture }); mat.uniforms = { myCustomUniform: { value: 10 }, } mat.tile({ // ... });` | `TilemapMaterial.extendClass(THREE.MeshPhongMaterial).uniforms` | src/TilemapMaterial.ts:140 |

## Methods

### customProgramCacheKey()

> **customProgramCacheKey**(): `string`

Overrides `THREE.Material.onBeforeCompile()`.
https://threejs.org/docs/?q=Material#api/en/materials/Material.customProgramCacheKey

Returns a custom shader cache key identifying the base
material and tiling type. When inheriting from this class
and overriding this method, ensure to adopt the original
key to prevent stale shaders across different configurationsL

```
customProgramCacheKey() {
  const originalKey = super.customProgramCacheKey();
  return `${originalKey}-${myKey}`;
}
```

#### Returns

`string`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).customProgramCacheKey`

#### Defined in

src/TilemapMaterial.ts:222

***

### injectShaderFragments()

> **injectShaderFragments**(`shader`): `void`

Injects tiling shader fragments into the material's original
shader program.

#### Parameters

| Parameter | Type | Description |
| ------ | ------ | ------ |
| `shader` | `WebGLProgramParametersWithUniforms` | The shader provided by the renderer. |

#### Returns

`void`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).injectShaderFragments`

#### Defined in

src/TilemapMaterial.ts:259

***

### mergeUniforms()

> **mergeUniforms**(`shader`?): `void`

Used internally to merge pre-existing uniforms after the
shader is (re-)compiled.

#### Parameters

| Parameter | Type | Description |
| ------ | ------ | ------ |
| `shader`? | `WebGLProgramParametersWithUniforms` | The shader provided by the renderer. |

#### Returns

`void`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).mergeUniforms`

#### Defined in

src/TilemapMaterial.ts:315

***

### onBeforeCompile()

> **onBeforeCompile**(`shader`): `void`

Overrides `THREE.Material.onBeforeCompile()`.
https://threejs.org/docs/?q=Material#api/en/materials/Material.onBeforeCompile

Injects tiling shader fragments into the material's original
shader program. When inheriting from this class and overriding
this method, ensure to call `super.onBeforeCompile()`
or `this.injectShaderFragments()` to ensure the tiling shader
artifacts are injected.

```
onBeforeCompile(shader) {
  // My shader manipulation logic here...
  this.injectShaderFragments(shader);
}
```

#### Parameters

| Parameter | Type | Description |
| ------ | ------ | ------ |
| `shader` | `WebGLProgramParametersWithUniforms` | The shader provided by the renderer. |

#### Returns

`void`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).onBeforeCompile`

#### Defined in

src/TilemapMaterial.ts:247

***

### setTilingOptions()

> **setTilingOptions**(`options`): `void`

Used internally to merge `ITilemapTilingOptions` from`.tile()`
with Required<ITilemapTilingOptions<THREE.Vector2>> on
`this.tiling`.

#### Parameters

| Parameter | Type | Description |
| ------ | ------ | ------ |
| `options` | [`ITilemapTilingOptions`](../interfaces/ITilemapTilingOptions.md)\<`Vector2Like`\> | Tiling options to set. |

#### Returns

`void`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).setTilingOptions`

#### Defined in

src/TilemapMaterial.ts:285

***

### tile()

> **tile**(`options`): `void`

Sets the tiling options:

```
const tilemap = new THREE.Mesh(
  new THREE.PlaneGeometry(10, 10),
  new TilemapMeshBasicMaterial({ map: myTileset }),
);
tilemap.material.tile({
  tile: [1, 2, 3, 4, 5, 6, 7, 8, 9],
  tileSize: { x: 16, y: 16 },
  tilesetSize: { x: 96, y: 80 },
});
myScene.add(tilemap);
```

#### Parameters

| Parameter | Type | Description |
| ------ | ------ | ------ |
| `options` | [`ITilemapTilingOptions`](../interfaces/ITilemapTilingOptions.md)\<`Vector2Like`\> | Tiling options to set. |

#### Returns

`void`

#### Inherited from

`TilemapMaterial.extendClass(THREE.MeshPhongMaterial).tile`

#### Defined in

src/TilemapMaterial.ts:167