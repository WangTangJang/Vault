枚举示例
``` java
// 定义一个枚举类型
enum Day {
    // 枚举常量
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}

public class EnumExample {

    // 枚举常量
    NULL_ERROR(40001, "请求数据为空", ""),
    NOT_LOGIN(40100, "未登录", ""),
    NO_AUTH(40101, "无权限", ""),

    SYSTEM_ERROR(50000, "系统内部异常", "");
    public static void main(String[] args) {
        // 使用枚举常量
        Day today = Day.WEDNESDAY;
	
        // 使用枚举常量的方法
        switch (today) {
            case MONDAY:
                System.out.println("周一，加油！");
                break;
            case WEDNESDAY:
                System.out.println("周三，中途休息！");
                break;
            case FRIDAY:
                System.out.println("周五，快到周末！");
                break;
            default:
                System.out.println("其他天，平常心！");
        }

        // 遍历枚举常量
        System.out.println("所有天：");
        for (Day day : Day.values()) {
            System.out.println(day);
        }
    }
}

```