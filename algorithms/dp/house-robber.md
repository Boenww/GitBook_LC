# house robber

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//O(n) space
public int rob(int[] nums) {     
    if (nums.length == 0) {
        return 0;
    } else if (nums.length == 1) {
        return nums[0];
    }

    int[] dp = new int[nums.length];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);
    for (int i = 2; i < nums.length; i++) {
        dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
    }

    return dp[dp.length - 1];
}

//O(1) space
public int rob(int[] nums) {
    int prev = 0, cur = 0;
    for (int i = 0; i < nums.length; i++) {
        int tmp = cur;
        cur = Math.max(cur, prev + nums[i]);
        prev = tmp;
    }
    
    return cur;
}
```
{% endtab %}
{% endtabs %}

