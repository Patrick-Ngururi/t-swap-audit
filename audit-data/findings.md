## Informationals

### [I-1]`PoolFactory::PoolFactory___PoolDoesNotExist` error is not used and should be removed.

```diff
- error PoolFactory__PoolDoesNotExist(address tokenAddress);
```

### [I-2] `PoolFactory::constructor` Lacking zero address check

```diff
    constructor(address wethToken) {
+       if(wethToken ==address(0)){
+           revert();
+        }       
        i_wethToken = wethToken;
    }
```

### [I-3] `PoolFactory::createPool` should use `.symbol()` instead of `.name()`

```diff
- string memory liquidityTokenSymbol = string.concat("ts", IERC20(tokenAddress).name());
+ string memory liquidityTokenSymbol = string.concat("ts", IERC20(tokenAddress).symbol());
```

### [I-4] `TSwapPool::constructor` Lacking zero address check - `wethToken` & `poolToken`

```diff
constructor(
    address poolToken,
    address wethToken,
    string memory liquidityTokenName,
    string memory liquidityTokenSymbol
)
    ERC20(liquidityTokenName, liquidityTokenSymbol)
{
+   if(wethToken || poolToken == address(0)){
+       revert();
+   }
    i_wethToken = IERC20(wethToken);
    i_poolToken = IERC20(poolToken);
}
```

### [I-5] `TSwapPool` events should be indexed

```diff
- event Swap(address indexed swapper, IERC20 tokenIn, uint256 amountTokenIn, IERC20 tokenOut, uint256 amountTokenOut);
+ event Swap(address indexed swapper, IERC20 indexed tokenIn, uint256 amountTokenIn, IERC20 indexed tokenOut, uint256 amountTokenOut);
```