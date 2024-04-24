### @Mapper

```java
@Mapper
public interface UserMapper {
	User getUserById(Long id);
	void insertUser(User user);
	void updateUser(User user);
	void deleteUser(Long id);
}
```

```xml
<mapper namespace="com.example.UserMapper">

	<select id="getUserById" resultType="com.example.User">
		SELECT * FROM users WHERE id = #{id}
	</select>

	<insert id="insertUser" parameterType="com.example.User">
		INSERT INTO users (username, email) VALUES (#{username}, #{email})
	</insert>

	<update id="updateUser" parameterType="com.example.User">
		UPDATE users SET username = #{username}, email = #{email} WHERE id = #{id}
	</update>

	<delete id="deleteUser" parameterType="Long">
		DELETE FROM users WHERE id = #{id}
	</delete>

</mapper>
```

* Mapper 인터페이스와 XML 파일을 연결하여 MyBatis가 SQL 쿼리를 실행하는 방법을 정의한다. 여기서 인터페이스는 SQL 쿼리를 호출하는 메서드이고, XML 파일은 이러한 메서드와 SQL 쿼리를 매핑한다.
