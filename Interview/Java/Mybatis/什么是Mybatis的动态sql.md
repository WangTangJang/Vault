MyBatis 的动态 SQL 是一种能够根据不同条件生成不同 SQL 语句的特性，这使得 SQL 语句的构建更加灵活和可重用。在 MyBatis 中，动态 SQL 主要通过 XML 配置文件中的一些特定标签来实现，也可以通过注解实现。

以下是 MyBatis 中常用的一些动态 SQL 标签：

1. **`<if>` 标签：**
   - `<if>` 标签用于条件判断，根据条件的成立与否动态地包含或排除部分 SQL 语句。

   ```xml
   <select id="getUsers" parameterType="map" resultType="User">
       SELECT * FROM users
       WHERE
       <if test="name != null">
           AND name = #{name}
       </if>
       <if test="age != null">
           AND age = #{age}
       </if>
   </select>
   ```

2. **`<choose>`、`<when>`、`<otherwise>` 标签：**
   - `<choose>` 标签类似于 Java 中的 switch 语句，`<when>` 标签表示条件分支，`<otherwise>` 标签表示默认分支。

   ```xml
   <select id="getUser" parameterType="int" resultType="User">
       SELECT *
       <choose>
           <when test="id != null">
               FROM users WHERE id = #{id}
           </when>
           <when test="username != null">
               FROM users WHERE username = #{username}
           </when>
           <otherwise>
               FROM users WHERE email = #{email}
           </otherwise>
       </choose>
   </select>
   ```

3. **`<trim>` 标签：**
   - `<trim>` 标签用于去除或包含 SQL 语句中的不必要的空白字符，通常用于处理 SQL 语句的动态拼接。

   ```xml
   <update id="updateUser" parameterType="User">
       UPDATE users
       <trim prefix="SET" suffixOverrides=",">
           <if test="name != null">name = #{name},</if>
           <if test="age != null">age = #{age},</if>
           <if test="email != null">email = #{email},</if>
       </trim>
       WHERE id = #{id}
   </update>
   ```

4. **`<foreach>` 标签：**
   - `<foreach>` 标签用于循环处理集合或数组，生成对应的 SQL 语句片段，常用于 `IN` 子句的构建。

   ```xml
   <select id="getUsersByIds" parameterType="List" resultType="User">
       SELECT * FROM users
       WHERE id IN
       <foreach item="id" collection="ids" open="(" separator="," close=")">
           #{id}
       </foreach>
   </select>
   ```

这些动态 SQL 标签可以组合使用，使得 SQL 语句的构建更加灵活，适应不同的查询条件和场景。