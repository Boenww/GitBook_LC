# valid ip address

Write a function to check whether an input string is a valid IPv4 address or IPv6 address or neither.

**IPv4** addresses are canonically represented in dot-decimal notation, which consists of four decimal numbers, each ranging from 0 to 255, separated by dots \("."\), e.g.,`172.16.254.1`;

Besides, leading zeros in the IPv4 is invalid. For example, the address `172.16.254.01` is invalid.

**IPv6** addresses are represented as eight groups of four hexadecimal digits, each group representing 16 bits. The groups are separated by colons \(":"\). For example, the address `2001:0db8:85a3:0000:0000:8a2e:0370:7334` is a valid one. Also, we could omit some leading zeros among four hexadecimal digits and some low-case characters in the address to upper-case ones, so `2001:db8:85a3:0:0:8A2E:0370:7334` is also a valid IPv6 address\(Omit leading zeros and using upper cases\).

However, we don't replace a consecutive group of zero value with a single empty group using two consecutive colons \(::\) to pursue simplicity. For example, `2001:0db8:85a3::8A2E:0370:7334` is an invalid IPv6 address.

Besides, extra leading zeros in the IPv6 is also invalid. For example, the address `02001:0db8:85a3:0000:0000:8a2e:0370:7334` is invalid.

{% tabs %}
{% tab title="Notes" %}
* check the number of the delimiter
* the "octet" could be negative\(overflow\)
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public String validIPAddress(String IP) {
        if (validIPv4(IP)) {
            return "IPv4";
        }
        
        if (validIPv6(IP)) {
            return "IPv6";
        }
        
        return "Neither";
    }
    
    public boolean validIPv4(String IP) {
        if (IP == null || IP.length() == 0 || numberOfDelimiter(IP, ".") != 3) {
            return false;
        }
        
        String[] address = IP.split("\\."); //special character
        if (address.length != 4) {
            return false;
        }
        
        for (String str: address) {
            if (str.length() == 0 || (str.length() > 1 && str.charAt(0) == '0')) {
                return false;
            }
            
            int num = 0;
            for (int i = 0; i < str.length(); i++) {
                char cur = str.charAt(i);
                if (cur < '0' || cur > '9') {
                    return false;
                }
                
                num = num * 10 + cur - '0';
            }
            
            
            if (num > 255 || num < 0) { //overflow
                return false;
            }
        }
        
        return true;
    }
    
    public boolean validIPv6(String IP) {
        if (IP == null || IP.length() == 0 || numberOfDelimiter(IP, ":") != 7) {
            return false;
        }
        
        String[] address = IP.split(":");
        if (address.length != 8) {
            return false;
        }
        
        for (String str: address) {
            if (str.length() == 0 || str.length() > 4) {
                return false;
            }
            
            for (int i = 0; i < str.length(); i++) {
                char cur = str.charAt(i);
                if (!((cur <= '9' && cur >= '0') || (cur <= 'F' && cur >= 'A') || (cur <= 'f' && cur >= 'a'))) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
    public int numberOfDelimiter(String IP, String delimiter) {
        int count = 0;
        for (int i = 0; i < IP.length() - delimiter.length() + 1; i++) {
            if (IP.substring(i, i + delimiter.length()).equals(delimiter)) {
                count++;
            }
        }
        
        return count;
    }
}
```
{% endtab %}
{% endtabs %}

