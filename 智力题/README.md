1. > **一共有1000瓶药水，其中1瓶有毒药。已知小白鼠喝毒药后会一天内死亡，若想一天内找到毒药，最少需要几只小白鼠？**

   答案：10只。

   解析：

   `0 000 000 001`表示1号老鼠喝了药水1；

   `0 000 000 010`表示2号老鼠喝了药水2；

   `0 000 000 011`表示1号、2号老鼠喝了药水3；

   ... ...

   `1 111 101 000`表示4、6、7、8、9、10号老鼠喝了药水1000；

   相当于用二进制数的每一位代表一只小白鼠，使用10只小白鼠组合了1000个二进制数字。观察哪几只小白鼠死亡，即可对应二进制数字转换成十进制就是有毒药水的编号。

2. > **抢30的双人游戏，游戏规则是：第一个喊“1”或”2“，第二个人接着往下喊一个或两个数字，然后再轮到第一个人。两人轮流下去，最后喊”30“的人获胜。问如果要获胜，喊数字的最佳策略是什么？**

   答案：喊3的倍数。

   解析：

   倒着分析，其实喊27的时候，就已经决定胜负了。假设A喊了27，B只能喊28或29或28、29，下个回合，A一定可以喊30。也就是说，喊27的人一定能获胜。同理再倒着分析，喊24的人一定能获胜。也就是说喊3的倍数的人必胜。最后发现谁先喊，谁就必输，因为第一个人无论喊几个数字，第二个人都会喊到3。所以不能第一个喊数字。

3. > 一块金子，只能切两刀，请问如何给一个人发一周的工资？

   答案：切成1、2、4三份。

   解析：第一天切一份给工人；第二天切两份给工人，工人找零一份回来；第三天把找零回来的一份再给工人；第四天把剩下的四份给工人，工人找零回来之前的两份和一份；第五天把找零回来的一份给工人；第六天把找零回来的两份给工人，工人再找零回来一份；第七天把找零回来的最后一份给工人。

4. > 一个圆环上有100个灯泡，灯泡有亮和暗两种状态。按下一个灯泡的开关可以改变它和与它相邻的两个灯泡的状态。设计一种算法，对于任意初始状态，使得所有灯泡全亮。

   解析：把灯泡编号1~100。

   - **步骤一：将灯泡变为全亮或只剩一个为暗**

     从1循环到98，遇到暗的则按它下一个，使之变亮。循环完毕，1~98必然全亮。99和100可能为亮亮、暗亮、亮暗、暗暗四种状态。

     - 亮亮：满足题目要求
     - 暗亮、亮暗：达到只剩一个为暗的状态
     - 暗暗：则按下编号100的灯泡，使编号99、100变为亮，编号1的灯泡变为暗，从而达到只剩一个为暗的状态

   - **步骤二：将灯泡变为全暗**

     由于灯泡是环形摆放，我们指定暗的灯泡为编号1，将剩下99个亮着的灯泡每3个为一组，按下每组中间的灯泡后，使得所有灯泡都变暗。

   - **步骤三：将灯泡变为全亮**

     将所有灯泡按一下，灯泡变为全亮。