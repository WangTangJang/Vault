在Redis中，脚本是由[[Lua语言]]编写的一段代码，它可以在服务器端原子性地执行。Redis提供了`EVAL`、`EVALSHA`和`SCRIPT`等命令用于处理Lua脚本。
### 执行脚本：

1. **EVAL命令：**
   - 使用`EVAL`命令可以在Redis服务器上执行一段Lua脚本。语法如下：

     ```redis
     EVAL script numkeys key [key ...] arg [arg ...]
     ```

     - `script`：Lua脚本。
     - `numkeys`：脚本中引用的键的数量。
     - `key [key ...]`：脚本中引用的键。
     - `arg [arg ...]`：传递给脚本的参数。

2. **EVALSHA命令：**
   - 与`EVAL`类似，但是通过脚本的SHA1散列值来执行脚本，可以提高执行效率。语法如下：

     ```redis
     EVALSHA sha1 numkeys key [key ...] arg [arg ...]
     ```

### 脚本管理：

1. **SCRIPT LOAD命令：**
   - 使用`SCRIPT LOAD`可以将Lua脚本加载到Redis服务器，返回一个脚本的SHA1散列值。之后可以使用`EVALSHA`执行该脚本。

     ```redis
     SCRIPT LOAD script
     ```

2. **SCRIPT EXISTS命令：**
   - 使用`SCRIPT EXISTS`检查给定的SHA1散列值是否已经加载到Redis服务器。

     ```redis
     SCRIPT EXISTS sha1 [sha1 ...]
     ```

3. **SCRIPT FLUSH命令：**
   - 使用`SCRIPT FLUSH`可以清除服务器上所有Lua脚本的缓存。

     ```redis
     SCRIPT FLUSH
     ```

4. **SCRIPT KILL命令：**
   - 使用`SCRIPT KILL`可以停止当前正在执行的Lua脚本。

     ```redis
     SCRIPT KILL
     ```

### 脚本示例：

```lua
-- 示例脚本：将键的值增加1
local currentValue = redis.call('GET', KEYS[1])
local newValue = tonumber(currentValue) + 1
redis.call('SET', KEYS[1], newValue)
return newValue
```

在这个示例中，Lua脚本通过`redis.call`函数调用Redis命令，并通过`KEYS`和`ARGV`参数引用传递给脚本的键和参数。

使用Lua脚本可以实现更复杂的逻辑，而且由于脚本在服务器端原子执行，可以保证一系列命令的原子性。然而，要注意脚本的执行会阻塞其他命令的执行，因此需要谨慎使用。