MyBatis 的懒加载（Lazy Loading）是一种延迟加载策略，它允许在需要的时候才加载相关联的数据，而不是在查询主对象时就立即加载所有的关联对象。这种机制有助于提高性能，减少不必要的数据库查询。

在 MyBatis 中，懒加载通常应用于关联对象的加载，即当访问某个对象的关联属性时才触发加载。懒加载主要通过在 MyBatis 映射文件中的 `<association>` 和 `<collection>` 标签中配置 `fetchType` 属性来实现。

以下是一个简单的示例，演示了如何在 MyBatis 中配置懒加载：

```xml
<!-- UserMapper.xml -->

<mapper namespace="com.example.UserMapper">

    <resultMap id="userResultMap" type="User">
        <id column="id" property="id"/>
        <result column="username" property="username"/>
        <!-- 配置懒加载 -->
        <association property="posts" javaType="List" column="id" select="com.example.PostMapper.getPostsByUserId" fetchType="lazy"/>
    </resultMap>

    <select id="getUserById" parameterType="int" resultMap="userResultMap">
        SELECT * FROM users WHERE id = #{id}
    </select>

</mapper>
```

在上面的示例中，`<association>` 标签用于配置懒加载。`fetchType` 属性设置为 `lazy`，这表示关联对象在需要访问时才会被加载。

使用懒加载时，注意以下几点：

1. **懒加载只在满足条件时触发：** 当访问关联属性时，MyBatis 会检查是否需要懒加载，只有在满足条件时才触发懒加载。

2. **懒加载需要保持连接：** 懒加载通常需要保持数据库连接的开启状态，因此需要在加载关联对象时保持连接处于打开状态。

3. **懒加载在事务内生效：** 懒加载通常需要在事务内生效，以确保能够加载相关联的对象。

懒加载是 MyBatis 提供的一个强大特性，可以提高性能并减少不必要的数据查询，但在使用时需要根据具体的业务场景谨慎配置。