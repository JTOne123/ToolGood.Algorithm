ToolGood.Algorithm
===================
ToolGood.Algorithm֧��`��������`��`Excel����`,��֧��`�Զ������`��

## ��������
``` csharp
    AlgorithmEngine engine = new AlgorithmEngine();
    double a=0.0;
    if (engine.Parse("1+2")) {
        a = (double)engine.Evaluate();
    }
    var c = engine.TryEvaluate("2+3", 0);
    var d = engine.TryEvaluate("count({1,2,3,4})", 0);//{}��������,����:4
    var s = engine.TryEvaluate("'aa'&'bb'", ""); //�ַ�������,����:aabb
    var r = engine.TryEvaluate("(1=1)*9+2", 0); //����:11
    var d = engine.TryEvaluate("'2016-1-1'+1", DateTime.MinValue); //��������:2016-1-2
    var t = engine.TryEvaluate("'2016-1-1'+9*'1:0'", DateTime.MinValue);//��������:2016-1-1 9:0
```
֧�ֳ���`pi`,`e`,`true`,`false`��

����Ĭ��Ϊ`Excel����`���������c#������������`UseExcelIndex`Ϊ`false`��

## �Զ������
``` csharp
    //����Բ����Ϣ
    public class Cylinder : AlgorithmEngine
    {
        private int _radius;
        private int _height;
        public Cylinder(int radius, int height)
        {
            _radius = radius;
            _height = height;
        }

        protected override Operand GetParameter(Operand curOpd)
        {
            if (curOpd.Parameter == "[�뾶]") {
                return new Operand(OperandType.NUMBER, _radius);
            }
            if (curOpd.Parameter == "[ֱ��]") {
                return new Operand(OperandType.NUMBER, _radius * 2);
            }
            if (curOpd.Parameter == "[��]") {
                return new Operand(OperandType.NUMBER, _height);
            }
            return base.GetParameter(curOpd);
        }
    }
    //���÷���
    Cylinder c = new Cylinder(3, 10);
    c.TryEvaluate("[�뾶]*[�뾶]*pi()", 0.0);      //Բ�����
    c.TryEvaluate("[ֱ��]*pi()", 0.0);            //Բ�ĳ�
    c.TryEvaluate("[�뾶]*[�뾶]*pi()*[��]", 0.0); //Բ�����
```


## Excel����
������`�߼�����`��`��ѧ�����Ǻ���`��`�ı�����`��`ͳ�ƺ���`��`������ʱ�亯��`

ע�����������ִ�Сд,�������ŵĲ�����ʡ��,ʾ���ķ���ֵ,����Ϊ����ֵ��
#### �߼�����
<table>
    <tr><td>������</td><td>˵��</td><td>ʾ��</td></tr>
    <tr>
        <td>IF</td><td>if(��������,��ֵ,[��ֵ])<br>ִ�����ֵ�ж�,�����߼���������ֵ,���ز�ͬ�����</td>
        <td>if(1=1,1,2) <br>>>1</td>
    </tr>
    <tr>
        <td>IFERROR</td><td>ifError(��������,��ֵ,[��ֵ])<br>�����ʽ����������򷵻���ָ����ֵ�����򷵻ع�ʽ�����</td>
        <td>iferror(1/0,1,2) <br>>>1</td>
    </tr>
    <tr>
        <td>IFNUMBER</td><td>ifNumber(��������,��ֵ,[��ֵ])<br>ָ��Ҫִ�е��߼����</td>
        <td>ifnumber(4,1,2) <br>>>1</td>
    </tr>
    <tr>
        <td>IFTEXT</td><td>ifText(��������,��ֵ,[��ֵ])<br>ָ��Ҫִ�е��߼����</td>
        <td>iftext('a',1,2) <br>>>1</td>
    </tr>
    <tr>
        <td>ISNUMBER</td><td>isNumber(ֵ)<br>�ж��Ƿ�����,���� TRUE �� FALSE</td>
        <td>ISNUMBER(1) <br>>>true</td>
    </tr>
    <tr>
        <td>ISTEXT</td><td>isText(ֵ)<br>�ж��Ƿ�����,���� TRUE �� FALSE</td>
        <td>istext('1') <br>>>true </td>
    </tr>
    <tr>
        <td>AND</td><td>and(�߼�ֵ1,...)<br>������в�����ΪTRUE,�򷵻�TRUE</td>
        <td>and(1,2=2) <br>>>true</td>
    </tr>
    <tr>
        <td>OR</td><td>or(�߼�ֵ1,...)<br>�����һ����ΪTRUE,�򷵻�TRUE</td>
        <td>or(1,2=3) <br>>>true</td>
    </tr>
    <tr>
        <td>NOT</td><td>not(�߼�ֵ)<br>�Բ������߼�ֵ��</td>
        <td>NOT(true()) <br>>>false</td>
    </tr>
    <tr>
        <td>TRUE</td><td>true()<br>�����߼�ֵTRUE</td>
        <td>true() <br>>>true</td>
    </tr>
    <tr>
        <td>FALSE</td><td>false()<br>�����߼�ֵFALSE</td>
        <td>false() <br>>>false</td>
    </tr>
</table>

#### ��ѧ�����Ǻ���
<table>
    <tr><td>����</td><td>������</td><td>˵��</td><td>ʾ��</td></tr>
    <tr>
        <td rowspan="12">��<br><br>��<br><br>��<br><br>ѧ</td>
        <td>PI</td><td>pi()<br>���� PI ֵ</td>
        <td>pi() <br>>>3.141592654</td>
    </tr>
    <tr>
        <td>abs</td><td>abs(����)<br>�������ֵľ���ֵ</td>
        <td>abs(-1) <br>>>1</td>
    </tr>
    <tr>
        <td>QUOTIENT</td><td>quotient(����,������)<br>�����̵���������,�ú�������������̵�С�����֡�</td>
        <td>QUOTIENT(7,3) <br>>>2</td>
    </tr>
    <tr>
        <td>mod</td><td>mod(����,������)<br>�����������������</td>
        <td>MOD(7,3) <br>>>1</td>
    </tr>
    <tr>
        <td>SIGN</td><td>sign(����)<br>�������ֵķ��š�������Ϊ����ʱ���� 1,Ϊ��ʱ���� 0,Ϊ����ʱ���� -1��</td>
        <td>SIGN(-9) <br>>>-1</td>
    </tr>
   <tr>
        <td>SQRT</td><td>sqrt(����)<br>������ƽ����</td>
        <td>SQRT(9) <br>>>3</td>
    </tr>
    <tr>
        <td>TRUNC</td><td>trunc(����)<br>�����ֽ�βȡ��</td>
        <td>TRUNC(9.222) <br>>>9</td>
    </tr>
    <tr>
        <td>int</td><td>int(����)<br>�������������뵽��ӽ���������</td>
        <td>int(9.222) <br>>>9</td>
    </tr>
    <tr>
        <td>gcd</td><td>gcd(����1,...)<br>�������Լ��</td>
        <td>GCD(3,5,7) <br>>>1</td>
    </tr>
    <tr>
        <td>LCM</td><td>lcm(����1,...)<br>����������������С������</td>
        <td>LCM(3,5,7) <br>>>105</td>
    </tr>
    <tr>
        <td>combin</td><td>combin(����,������)<br>����Ӹ�����Ŀ�Ķ��󼯺�����ȡ���ɶ���������</td>
        <td>combin(10,2) <br>>>45</td>
    </tr>
    <tr>
        <td>PERMUT</td><td>permut(����,������)<br>���شӸ�����Ŀ�Ķ��󼯺���ѡȡ�����ɶ����������</td>
        <td>PERMUT(10,2) <br>>>990</td>
    </tr>
    <tr>
    <td rowspan="15">��<br><br>��<br><br>��<br><br>��</td>
        <td>degrees</td><td>degrees(����)<br>������ת��Ϊ��</td>
        <td>degrees(pi()) <br>>>180</td>
    </tr>
    <tr>
        <td>RADIANS</td><td>radians(��)<br>����ת��Ϊ����</td>
        <td>RADIANS(180) <br>>>3.141592654</td>
    </tr>
    <tr>
        <td>cos</td><td>cos(����)<br>�������ֵ�����ֵ</td>
        <td>cos(1) <br>>>0.540302305868</td>
    </tr>
    <tr>
        <td>cosh</td><td>cosh(����)<br>�������ֵ�˫������ֵ</td>
        <td>cosh(1) <br>>>1.54308063481</td>
    </tr>
    <tr>
        <td>SIN</td><td>sin(����)<br>���ظ����Ƕȵ�����ֵ</td>
        <td>sin(1) <br>>>0.84147098480</td>
    </tr>
    <tr>
        <td>SINH</td><td>sinh(����)<br>�������ֵ�˫������ֵ</td>
        <td>sinh(1) <br>>>1.1752011936</td>
    </tr>
    <tr>
        <td>TAN</td><td>tan(����)<br>�������ֵ�����ֵ</td>
        <td>tan(1) <br>>>1.55740772465</td>
    </tr>
    <tr>
        <td>TANH</td><td>tanh(����)<br>�������ֵ�˫������ֵ</td>
        <td>tanh(1) <br>>>0.761594155955</td>
    </tr>
    <tr>
        <td>acos</td><td>acos(��ֵ)<br>�������ֵķ�����ֵ</td>
        <td>acos(0.5) <br>>>1.04719755119</td>
    </tr>
    <tr>
        <td>acosh</td><td>acosh(��ֵ)<br>�������ֵķ�˫������ֵ</td>
        <td>acosh(1.5) <br>>>0.962423650119</td>
    </tr>
    <tr>
        <td>asin</td><td>asin(��ֵ)<br>�������ֵķ�����ֵ</td>
        <td>asin(0.5) <br>>>0.523598775598</td>
    </tr>
    <tr>
        <td>asinh</td><td>asinh(��ֵ)<br>�������ֵķ�˫������ֵ��</td>
        <td>asinh(1.5) <br>>>1.1947632172</td>
    </tr>
    <tr>
        <td>atan</td><td>atan(��ֵ)<br>�������ֵķ�����ֵ</td>
        <td>atan(1) <br>>>0.785398163397</td>
    </tr>
   <tr>
        <td>atanh</td><td>atanh(��ֵ)<br>���ز����ķ�˫������ֵ</td>
        <td>atanh(1) <br>>>0.549306144334</td>
    </tr>
    <tr>
        <td>atan2</td><td>atan2(��ֵ)<br>��X��Y���귵�ط�����</td>
        <td>atan2(1,2) <br>>>1.10714871779</td>
    </tr>
    <tr>
        <td rowspan="8">��<br><br>��<br><br>��<br><br>��</td>
        <td>ROUND</td><td>round(��ֵ,С��λ��)<br>����ĳ�����ְ�ָ��λ��ȡ��������֡�</td>
        <td>ROUND(4.333,2) <br>>>4.33</td>
    </tr>
    <tr>
        <td>ROUNDDOWN</td><td>roundDown(��ֵ,С��λ��)<br>������ֵ,���£�����ֵ��С�ķ����������֡�</td>
        <td>ROUNDDOWN(4.333,2) <br>>>4.33</td>
    </tr>
    <tr>
        <td>ROUNDUP</td><td>roundUp(��ֵ,С��λ��)<br>Զ����ֵ,���ϣ�����ֵ�����ķ����������֡�</td>
        <td>ROUNDUP(4.333,2) <br>>>4.34</td>
    </tr>
    <tr>
        <td>CEILING</td><td>ceiling(��ֵ,�������)<br>�������루�ؾ���ֵ����ķ���Ϊ��ӽ��� ������� �ı�����</td>
        <td>CEILING(4.333,0.1) <br>>>4.4</td>
    </tr>
    <tr>
        <td>floor</td><td>floor(��ֵ,�������)<br>��������,ʹ�������ӽ��� Significance �ı�����</td>
        <td>FLOOR(4.333,0.1) <br>>>4.3</td>
    </tr>
    <tr>
        <td>even</td><td>even(��ֵ)<br>�����ؾ���ֵ������ȡ������ӽ���ż����</td>
        <td>EVEN(3) <br>>>4</td>
    </tr>
    <tr>
        <td>ODD</td><td>odd(��ֵ)<br>��������������Ϊ��ӽ�����������</td>
        <td>ODD(3.1) <br>>>5</td>
    </tr>
    <tr>
        <td>MROUND</td><td>mround(��ֵ,�������)<br>����һ�����뵽���豶��������</td>
        <td>MROUND(13,5) <br>>>15</td>
    </tr>
    <tr>
        <td rowspan="2">��<br><br>��<br><br>��</td>
        <td>RAND</td><td>rand()<br>���� 0 �� 1 ֮�������� </td>
        <td>RAND() <br>>>0.2</td>
    </tr>
    <tr>
        <td>RANDBETWEEN</td><td>randBetween(��С����,�������)<br>���ش��ڵ���ָ������Сֵ,С��ָ�����ֵ֮���һ�����������</td>
        <td>RANDBETWEEN(2,44) <br>>>9</td>
    </tr>
    <tr>
        <td rowspan="11">��<br><br>/<br><br>��<br><br>��<br><br>/<br><br>��<br><br>��</td>
        <td>fact</td><td>fact(��ֵ)<br>�������Ľ׳�,һ�����Ľ׳˵��� 1*2*3*��* ������</td>
        <td>FACT(3) <br>>>6</td>
    </tr>
    <tr>
        <td>factdouble</td><td>factDouble(��ֵ)<br>�������ֵ�˫���׳�</td>
        <td>FACTDOUBLE(10) <br>>>3840</td>
    </tr>
    <tr>
        <td>POWER</td><td>power(��ֵ,��)<br>�������ĳ��ݽ��</td>
        <td>POWER(10,2) <br>>>100</td>
    </tr>
    <tr>
        <td>exp</td><td>exp(��)<br>����e��ָ��������</td>
        <td>exp(2) <br>>>7.389056099</td>
    </tr>
    <tr>
        <td>ln</td><td>ln(��ֵ)<br>�������ֵ���Ȼ����</td>
        <td>LN(4) <br>>>1.386294361</td>
    </tr>
    <tr>
        <td>log</td><td>log(��ֵ,[����])<br>�������ֵĳ��ö���,��ʡ�Ե���,Ĭ��Ϊ10</td>
        <td>LOG(100,10) <br>>>2</td>
    </tr>
    <tr>
        <td>LOG10</td><td>log10(��ֵ)<br>�������ֵ�10����</td>
        <td>LOG10(100) <br>>>2</td>
    </tr>
    <tr>
        <td>MULTINOMIAL</td><td>multinomial(��ֵ1,...)<br>���ز����͵Ľ׳���������׳˳˻��ı�ֵ</td>
        <td>MULTINOMIAL(1,2,3) <br>>>60</td>
    </tr>
    <tr>
        <td>PRODUCT</td><td>product(��ֵ1,...)<br>�������Բ�����ʽ�������������,�����س˻�ֵ��</td>
        <td>PRODUCT(1,2,3,4) <br>>>24</td>
    </tr>
    <tr>
        <td>SQRTPI</td><td>sqrtPi(��ֵ)<br>����ĳ���� PI �ĳ˻���ƽ����</td>
        <td>SQRTPI(3) <br>>>3.069980124</td>
    </tr>
    <tr>
        <td>SUMSQ</td><td>sumQq(��ֵ,...)<br>���ز�����ƽ����</td>
        <td>SUMSQ(1,2) <br>>>5</td>
    </tr>
</table>

#### �ı�����
<table>
    <tr><td>������</td><td>˵��</td><td>ʾ��</td></tr>
    <tr>
        <td>ASC</td><td>asc(�ַ���)<br>���ַ����ڵ�ȫ��Ӣ����ĸ����Ϊ����ַ�</td>
        <td>asc('������£ã�����') <br>>>abcABC123</td>
    </tr>
    <tr>
        <td>JIS / WIDECHAR</td><td>jis(�ַ���)<br>���ַ����еİ��Ӣ���ַ�����Ϊȫ���ַ�</td>
        <td>jis('abcABC123') <br>>>������£ã�����</td>
    </tr>
    <tr>
        <td>CHAR</td><td>jis(��ֵ)<br>�����ɴ�������ָ�����ַ�</td>
        <td>char(49) <br>>>1</td>
    </tr>
    <tr>
        <td>CLEAN</td><td>clean(�ַ���)<br>ɾ���ı������д�ӡ�������ַ�</td>
        <td>clean('\r112\t') <br>>>112</td>
    </tr>
    <tr>
        <td>CODE</td><td>code(�ַ���)<br>�����ı��ַ����е�һ���ַ������ִ���</td>
        <td>CODE("1") <br>>>49</td>
    </tr>
    <tr>
        <td>CONCATENATE</td><td>concatenate(�ַ���1,...)<br>�������ı���ϲ���һ���ı�����</td>
        <td>CONCATENATE('tt','11') <br>>>tt11</td>
    </tr>
    <tr>
        <td>EXACT</td><td>exact(�ַ���1,�ַ���2)<br>��������ı�ֵ�Ƿ���ȫ��ͬ</td>
        <td>EXACT("11","22") <br>>>false</td>
    </tr>
    <tr>
        <td>FIND</td><td>find(Ҫ���ҵ��ַ���,�����ҵ��ַ���,[��ʼλ��])<br>��һ�ı�ֵ�ڲ�����һ�ı�ֵ�����ִ�Сд�� </td>
        <td>FIND("11","12221122") <br>>>5</td>
    </tr>
    <tr>
        <td>FIXED</td><td>fixed(��ֵ,[С��λ��],[���޶��ŷָ���])<br>����������Ϊ���й̶�С��λ���ı���ʽ</td>
        <td>FIXED(4567.89,1) <br>>>4,567.9</td>
    </tr>
    <tr>
        <td>LEFT</td><td>left(�ַ���,[�ַ�����])<br>�����ı�ֵ����ߵ��ַ�</td>
        <td>LEFT('123222',3) <br>>>123</td>
    </tr>
    <tr>
        <td>LEN</td><td>len(�ַ���)<br>�����ı��ַ����е��ַ�����</td>
        <td>LEN('123222') <br>>>6</td>
    </tr>
    <tr>
        <td>LOWER</td><td>lower(�ַ���)<br>���ı�ת��ΪСд��ʽ</td>
        <td>LOWER('ABC') <br>>>abc</td>
    </tr>
    <tr>
        <td>MID</td><td>mid(�ַ���,��ʼλ��,�ַ�����)<br>���ı��ַ����е�ָ��λ���𷵻��ض��������ַ�</td>
        <td>MID('ABCDEF',2,3) <br>>>BCD</td>
    </tr>
    <tr>
        <td>PROPER</td><td>proper(�ַ���)<br>���ı�ֵ��ÿһ�����ʵ�����ĸ����Ϊ��д</td>
        <td>PROPER('abc abc') <br>>>Abc Abc</td>
    </tr>
    <tr>
        <td>REPLACE</td>
        <td>replace(ԭ�ַ���,��ʼλ��,�ַ�����,���ַ���)<br>
        replace(ԭ�ַ���,Ҫ�滻���ַ���, ���ַ���)<br>
        �滻�ı��ڵ��ַ�</td>
        <td>REPLACE("abccd",2,3,"2") <br>>>a2d<br>
        REPLACE("abccd","bc","2") <br>>>a2cd
        </td>
    </tr>
    <tr>
        <td>REPT</td><td>rept(�ַ���,�ظ�����)<br>�����������ظ��ı�</td>
        <td>REPT("q",3) <br>>>qqq</td>
    </tr>
    <tr>
        <td>RIGHT</td><td>right(�ַ���,[�ַ�����])<br>�����ı�ֵ���ұߵ��ַ�</td>
        <td>RIGHT("123q",3) <br>>>23q</td>
    </tr>
    <tr>
        <td>RMB</td><td>rmb(��ֵ)<br>������ת��Ϊ��д�����ı�</td>
        <td>rmb(12.3) <br>>>Ҽʰ��Ԫ����</td>
    </tr>
    <tr>
        <td>SEARCH</td><td>search(Ҫ�ҵ��ַ���,�����ҵ��ַ���,[��ʼλ��])<br>��һ�ı�ֵ�в�����һ�ı�ֵ�������ִ�Сд��</td>
        <td>SEARCH("aa","abbAaddd") <br>>>4</td>
    </tr>
    <tr>
        <td>SUBSTITUTE</td><td>substitute(�ַ���,ԭ�ַ���,���ַ���,[�滻���])<br>���ı��ַ����������ı��滻���ı�</td>
        <td>SUBSTITUTE("ababcc","ab","12") <br>>>1212cc</td>
    </tr>
    <tr>
        <td>T</td><td>t(��ֵ)<br>������ת��Ϊ�ı�</td>
        <td>T('123') <br>>>123</td>
    </tr>
    <tr>
        <td>TEXT</td><td>text(��ֵ,��ֵ��ʽ)<br>�������ֵĸ�ʽ��������ת��Ϊ�ı�</td>
        <td>TEXT(123,"0.00") <br>>>123.00</td>
    </tr>
    <tr>
        <td>TRIM</td><td>trim(�ַ���)<br>ɾ���ı��еĿո�</td>
        <td>TRIM(" 123 123 ")<br>>>123 123</td>
    </tr>
    <tr>
        <td>UPPER</td><td>upper(�ַ���)<br>���ı�ת��Ϊ��д��ʽ</td>
        <td>UPPER("abc") <br>>>ABC</td>
    </tr>
    <tr>
        <td>VALUE</td><td>value(�ַ���)<br>���ı�����ת��Ϊ����</td>
        <td>VALUE("123") <br>>>123</td>
    </tr>
</table>

#### ������ʱ�亯��
<table>
    <tr><td>������</td><td>˵��</td><td>ʾ��</td></tr>
    <tr>
        <td>DATEVALUE</td><td>dateValue(�ַ���)<br>���ı���ʽ������ת��Ϊ���к�</td>
        <td>DATEVALUE("2017-01-02") <br>>>2017-01-02</td>
    </tr>
    <tr>
        <td>TIMEVALUE</td><td>timeValue(�ַ���)<br>���ı���ʽ��ʱ��ת��Ϊ���к�</td>
        <td>TIMEVALUE("12:12:12") <br>>>12:12:12</td>
    </tr>
    <tr>
        <td>DATE</td><td>date(��,��,��,[ʱ],[��],[��])<br>�����ض����ڵ����к�</td>
        <td>DATE(2016,1,1) <br>>>2016-01-01</td>
    </tr>
    <tr>
        <td>TIME</td><td>time(ʱ,��,��)<br>�����ض�ʱ������к�</td>
        <td>TIME(12,13,14) <br>>>12:13:14</td>
    </tr>
    <tr>
        <td>NOW</td><td>now()<br>���ص�ǰ���ں�ʱ������к�</td>
        <td>NOW() <br>>>2017-01-07 11:00:00</td>
    </tr>
    <tr>
        <td>TODAY</td><td>today()<br>���ؽ������ڵ����к�</td>
        <td>TODAY() <br>>>2017-01-07</td>
    </tr>
    <tr>
        <td>YEAR</td><td>year(����)<br>�����к�ת��Ϊ��</td>
        <td>YEAR(NOW()) <br>>>2017</td>
    </tr>
    <tr>
        <td>MONTH</td><td>month(����)<br>�����к�ת��Ϊ��</td>
        <td>MONTH(NOW()) <br>>>1</td>
    </tr>
    <tr>
        <td>DAY</td><td>day(����)<br>�����к�ת��Ϊ�·��е���</td>
        <td>DAY(NOW()) <br>>>7</td>
    </tr>
    <tr>
        <td>HOUR</td><td>hour(����)<br>�����к�ת��ΪСʱ</td>
        <td>HOUR(NOW()) <br>>>11</td>
    </tr>
    <tr>
        <td>MINUTE</td><td>minute(����)<br>�����к�ת��Ϊ����</td>
        <td>MINUTE(NOW()) <br>>>12</td>
    </tr>
    <tr>
        <td>SECOND</td><td>second(����)<br>�����к�ת��Ϊ��</td>
        <td>SECOND(NOW()) <br>>>34</td>
    </tr>
    <tr>
        <td>WEEKDAY</td><td>second(����)<br>�����к�ת��Ϊ���ڼ�</td>
        <td>WEEKDAY(date(2017,1,7)) <br>>>7</td>
    </tr>
    <tr>
        <td>DATEDIF</td><td>dateDif(��ʼ����,��������,����Y/M/D/YD/MD/YM)<br>������������֮����������</td>
        <td>DATEDIF("1975-1-30","2017-1-7","Y") <br>>>41</td>
    </tr>
    <tr>
        <td>DAYS360</td><td>days360(��ʼ����,��������,[ѡ��0/1])<br>��һ�� 360 ��Ϊ��׼�����������ڼ������</td>
        <td>DAYS360('1975-1-30','2017-1-7') <br>>>15097</td>
    </tr>
    <tr>
        <td>EDATE</td><td>eDate(��ʼ����,����)<br>�������ڱ�ʾ��ʼ����֮ǰ��֮�����������ڵ����к�</td>
        <td>EDATE("2012-1-31",32) <br>>>2014-09-30</td>
    </tr>
    <tr>
        <td>EOMONTH</td><td>eoMonth(��ʼ����,����)<br>����ָ������֮ǰ��֮����·ݵ����һ������к�</td>
        <td>EOMONTH("2012-2-1",32) <br>>>2014-10-31</td>
    </tr>
    <tr>
        <td>NETWORKDAYS</td><td>netWorkdays(��ʼ����,��������,[����])<br>������������֮���ȫ����������</td>
        <td>NETWORKDAYS("2012-1-1","2013-1-1") <br>>>262</td>
    </tr>
    <tr>
        <td>WORKDAY</td><td>workday(��ʼ����,����,[����])<br>����ָ�������ɸ�������֮ǰ��֮������ڵ����к�</td>
        <td>WORKDAY("2012-1-2",145) <br>>>2012-07-23</td>
    </tr>
    <tr>
        <td>WEEKNUM</td><td>weekNum(����,[���ͣ�1/2])<br>�����к�ת��Ϊһ������Ӧ������</td>
        <td>WEEKNUM("2016-1-3") <br>>>2</td>
    </tr>
</table>

#### ͳ�ƺ���
<table>
    <tr><td>������</td><td>˵��</td><td>ʾ��</td></tr>
    <tr>
        <td>MAX</td><td>max(��ֵ)<br>���ز����б��е����ֵ</td>
        <td>max(1,2,3,4,2,2,1,4) <br>>>4</td>
    </tr>
    <tr>
        <td>MEDIAN</td><td>median(��ֵ)<br>���ظ������ֵ���ֵ</td>
        <td>MEDIAN(1,2,3,4,2,2,1,4) <br>>>2</td>
    </tr>
    <tr>
        <td>MIN</td><td>min(��ֵ)<br>���ز����б��е���Сֵ</td>
        <td>MIN(1,2,3,4,2,2,1,4) <br>>>1</td>
    </tr>
    <tr>
        <td>QUARTILE</td><td>quartile(��ֵ,�ķ�λ��0-4)<br>�������ݼ����ķ�λ��</td>
        <td>QUARTILE({1,2,3,4,2,2,1,4},0) <br>>>1</td>
    </tr>
    <tr>
        <td>MODE</td><td>mode(��ֵ1,...)<br>�����������г���Ƶ��������ֵ</td>
        <td>MODE(1,2,3,4,2,2,1,4) <br>>>2</td>
    </tr>
    <tr>
        <td>LARGE</td><td>large(����,K)<br>�������ݼ��е� k �����ֵ</td>
        <td>LARGE({1,2,3,4,2,2,1,4},3) <br>>>3</td>
    </tr>
    <tr>
        <td>SMALL</td><td>small(��ֵ,K)<br>�������ݼ��е� k ����Сֵ</td>
        <td>SMALL({1,2,3,4,2,2,1,4},3) <br>>>2</td>
    </tr>
    <tr>
        <td>PERCENTILE</td><td>percentile(��ֵ,K)<br>���������еĵ� k ���ٷ�λֵ</td>
        <td>PERCENTILE({1,2,3,4,2,2,1,4},0.4) <br>>>2</td>
    </tr>
    <tr>
        <td>PERCENTRANK</td><td>percentRank(��ֵ,K)<br>�������ݼ���ֵ�İٷֱ���λ</td>
        <td>PERCENTRANK({1,2,3,4,2,2,1,4},3) <br>>>0.714</td>
    </tr>
    <tr>
        <td>AVERAGE</td><td>average(��ֵ1,...)<br>���ز�����ƽ��ֵ</td>
        <td>AVERAGE(1,2,3,4,2,2,1,4) <br>>>2.375</td>
    </tr>
    <tr>
        <td>AVERAGEIF</td><td>averageIf(��ֵ1,...)<br>���ز�����ƽ��ֵ</td>
        <td>AVERAGEIF({1,2,3,4,2,2,1,4},'>1') <br>>>2.833333333</td>
    </tr>
    <tr>
        <td>GEOMEAN</td><td>geoMean(��ֵ1,...)<br>�����������������ļ���ƽ��ֵ</td>
        <td>GEOMEAN(1,2,3,4) <br>>>2.213363839</td>
    </tr>
    <tr>
        <td>HARMEAN</td><td>harMean(��ֵ1,...)<br>�������ݼ��ϵĵ���ƽ��ֵ</td>
        <td>HARMEAN(1,2,3,4) <br>>>1.92</td>
    </tr>
    <tr>
        <td>COUNT</td><td>count(��ֵ1,...)<br>��������б������ֵĸ���</td>
        <td>COUNT(1,2,3,4,2,2,1,4) <br>>>8</td>
    </tr>
    <tr>
        <td>COUNTIF</td><td>countIf(��ֵ1,...)<br>��������б������ֵĸ���</td>
        <td>COUNTIF({1,2,3,4,2,2,1,4},'>1') <br>>>6</td>
    </tr>
    <tr>
        <td>SUM</td><td>sum(��ֵ1,...)<br>������������֮�͡�</td>
        <td>SUM(1,2,3,4) <br>>>10</td>
    </tr>
    <tr>
        <td>SUMIF</td><td>sumIf(��ֵ1,...)<br>������������֮��</td>
        <td>SUMIF({1,2,3,4,2,2,1,4},'>1') <br>>>17</td>
    </tr>
    <tr>
        <td>AVEDEV</td><td>aveDev(��ֵ1,...)<br>�������ݵ�����ƽ��ֵ�ľ���ƫ���ƽ��ֵ</td>
        <td>AVEDEV(1,2,3,4,2,2,1,4) <br>>>0.96875</td>
    </tr>
    <tr>
        <td>STDEV</td><td>stDev(��ֵ1,...)<br>�������������׼ƫ��</td>
        <td>STDEV(1,2,3,4,2,2,1,4) <br>>>1.1877349391654208</td>
    </tr>
    <tr>
        <td>STDEVP</td><td>stDevp(��ֵ1,...)<br>�������������������ı�׼ƫ��</td>
        <td>STDEVP(1,2,3,4,2,2,1,4) <br>>>1.1110243021644486</td>
    </tr>
    <tr>
        <td>DEVSQ</td><td>devSq(��ֵ1,...)<br>����ƫ���ƽ����</td>
        <td>DEVSQ(1,2,3,4,2,2,1,4) <br>>>9.875</td>
    </tr>
    <tr>
        <td>VAR</td><td>var(��ֵ1,...)<br>�����������㷽��</td>
        <td>VAR(1,2,3,4,2,2,1,4) <br>>>1.4107142857142858</td>
    </tr>
    <tr>
        <td>VARP</td><td>varp(��ֵ1,...)<br>������������������㷽��</td>
        <td>VARP(1,2,3,4,2,2,1,4) <br>>>1.234375</td>
    </tr>
    <tr>
        <td>NORMDIST</td><td>normDist(��ֵ,����ƽ��ֵ,��׼ƫ��,�������ͣ�0/1)<br>������̬�ۻ��ֲ�</td>
        <td>NORMDIST(3,8,4,1) <br>>>0.105649774</td>
    </tr>
    <tr>
        <td>NORMINV</td><td>normInv(�ֲ�����,����ƽ��ֵ,��׼ƫ��)<br>���ط���̬�ۻ��ֲ�</td>
        <td>NORMINV(0.8,8,3) <br>>>10.5248637</td>
    </tr>
    <tr>
        <td>NormSDist</td><td>normSDist(��ֵ)<br>���ر�׼��̬�ۻ��ֲ�����,�÷ֲ���ƽ��ֵΪ 0,��׼ƫ��Ϊ 1��</td>
        <td>NORMSDIST(1) <br>>>0.841344746</td>
    </tr>
    <tr>
        <td>NORMSINV</td><td>normInv(��ֵ)<br>���ط���׼��̬�ۻ��ֲ�</td>
        <td>NORMSINV(0.3) <br>>>-0.524400513</td>
    </tr>
    <tr>
        <td>BETADIST</td><td>betaDist(��ֵ,�ֲ�������,�ֲ�������)<br>���� Beta �ۻ��ֲ�����</td>
        <td>BETADIST(0.5,11,22) <br>>>0.97494877</td>
    </tr>
    <tr>
        <td>BETAINV</td><td>betaInv(��ֵ,�ֲ�������,�ֲ�������)<br>����ָ�� Beta �ֲ����ۻ��ֲ������ķ�����</td>
        <td>BETAINV(0.5,23,45) <br>>>0.336640759</td>
    </tr>
    <tr>
        <td>BINOMDIST</td><td>binomDist(����ɹ�����,�������,�ɹ�����,�������ͣ�0/1)<br>����һԪ����ʽ�ֲ�����</td>
        <td>BINOMDIST(12,45,0.5,0) <br>>>0.000817409</td>
    </tr>
    <tr>
        <td>EXPONDIST</td><td>exponDist(����ֵ,����ֵ,�������ͣ�0/1)<br>����ָ���ֲ�</td>
        <td>EXPONDIST(3,1,0) <br>>>0.049787068</td>
    </tr>
    <tr>
        <td>FDIST</td><td>fDist(��ֵX,�������ɶ�,��ĸ���ɶ�)<br>���� F ���ʷֲ�</td>
        <td>FDIST(0.4,2,3) <br>>>0.701465776</td>
    </tr>
    <tr>
        <td>FINV</td><td>fInv(�ֲ�����,�������ɶ�,��ĸ���ɶ�)<br>���� F ���ʷֲ��ķ�����</td>
        <td>FINV(0.7,2,3) <br>>>0.402651432</td>
    </tr>
    <tr>
        <td>FISHER</td><td>fisher(��ֵ)<br>���ص� x �� Fisher �任���ñ任����һ����̬�ֲ�����ƫб�ĺ���</td>
        <td>FISHER(0.68) <br>>>0.8291140383</td>
    </tr>
    <tr>
        <td>FISHERINV</td><td>fisherInv(��ֵ)<br>���� Fisher �任�ķ�����ֵ��</td>
        <td>FISHERINV(0.6) <br>>>0.537049567</td>
    </tr>
    <tr>
        <td>GAMMADIST</td><td>gammaDist(��ֵ,�ֲ�������,�ֲ�������,�������ͣ�0/1)<br>���� �� �ֲ�</td>
        <td>GAMMADIST(0.5,3,4,0) <br>>>0.001723627</td>
    </tr>
    <tr>
        <td>GAMMAINV</td><td>gammaInv(�ֲ�����,�ֲ�������,�ֲ�������)<br>���� �� �ۻ��ֲ������ķ�����</td>
        <td>GAMMAINV(0.2,3,4) <br>>>6.140176811</td>
    </tr>
    <tr>
        <td>GAMMALN</td><td>gammaLn(��ֵ)<br>���� �� �ۻ��ֲ������ķ�����</td>
        <td>GAMMALN(4) <br>>>1.791759469</td>
    </tr>
    <tr>
        <td>HYPGEOMDIST</td><td>hypgeomDist(�����ɹ�����,��������,��������ɹ�����,������������)<br>���س����ηֲ�</td>
        <td>HYPGEOMDIST(23,45,45,100) <br>>>0.08715016</td>
    </tr>
    <tr>
        <td>LOGINV</td><td>logInv(�ֲ�����,�㷨ƽ����,��׼ƫ��)<br>���� x �Ķ����ۻ��ֲ������ķ�����</td>
        <td>LOGINV(0.1,45,33) <br>>>15.01122624</td>
    </tr>
    <tr>
        <td>LognormDist</td><td>lognormDist(��ֵ,�㷨ƽ����,��׼ƫ��)<br>���ط�������̬�ֲ�</td>
        <td>LOGNORMDIST(15,23,45) <br>>>0.326019201</td>
    </tr>
    <tr>
        <td>NEGBINOMDIST</td><td>negbinomDist(ʧ�ܴ���,�ɹ����޴���,�ɹ�����)<br>���ظ�����ʽ�ֲ�</td>
        <td>NEGBINOMDIST(23,45,0.7) <br>>>0.053463314</td>
    </tr>
    <tr>
        <td>POISSON</td><td>poisson(��ֵ,�㷨ƽ����,�������ͣ�0/1)<br>���� Poisson �ֲ�</td>
        <td>POISSON(23,23,0) <br>>>0.082884384</td>
    </tr>
    <tr>
        <td>TDIST</td><td>tDist(��ֵ,���ɶ�,�������ͣ�1/2)<br>����ѧ���� t �ֲ�</td>
        <td>TDIST(1.2,24,1) <br>>>0.120925677</td>
    </tr>
    <tr>
        <td>TINV</td><td>tDist(�ֲ�����,���ɶ�)<br>����ѧ���� t �ֲ��ķ��ֲ�</td>
        <td>TINV(0.12,23) <br>>>1.614756561</td>
    </tr>
    <tr>
        <td>WEIBULL</td><td>weibull(��ֵ,�ֲ�������,�ֲ�������,�������ͣ�0/1)<br>���� Weibull �ֲ�</td>
        <td>WEIBULL(1,2,3,1) <br>>>0.105160683</td>
    </tr>

</table>


#### ���Ӻ��� ��C#����
<table>
    <tr><td>������</td><td>˵��</td><td>ʾ��</td></tr>
    <tr>
        <td>UrlEncode</td><td>UrlEncode(�ı�)<br> �� URL �ַ������б��롣</td> <td></td>
    </tr>
	<tr>
        <td>UrlDecode</td><td>UrlEncode(�ı�)<br> �� URL ������ַ���ת��Ϊ�ѽ�����ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>HtmlEncode</td><td>HtmlEncode(�ı�)<br> ���ַ���ת��Ϊ HTML ������ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>HtmlEncode</td><td>HtmlEncode(�ı�)<br>  ���ַ�����ʾ��ʽת��Ϊ HTML ������ַ����������ر�����ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Base64ToText</td><td>Base64ToText(�ı�)<br>Base64ToText(�ı�,��������)<br>   ��Base64ת��Ϊ�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Base64UrlToText</td><td>Base64UrlToText(�ı�)<br>Base64UrlToText(�ı�,��������)<br>   ��Url���͵�Base64 ת��Ϊ�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>TextToBase64</td><td>TextToBase64(�ı�)<br>TextToBase64(�ı�,��������)<br>   ���ַ���ת��ΪBase64�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>TextToBase64Url</td><td>TextToBase64Url(�ı�)<br>TextToBase64Url(�ı�,��������)<br>   ���ַ��� ת��ΪUrl���͵�Base64 �ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Regex</td><td>Regex(�ı�,ƥ���ı�)<br>Regex(�ı�,ƥ���ı�,����)<br>Regex(�ı�,ƥ���ı�,����,������)<br>   ������ƥ����ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>RegexRepalce</td><td>RegexRepalce(�ı�,ƥ���ı�,�滻�ı�)<br>  ƥ���滻�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>IsRegex<br>IsMatch</td><td>IsRegex(�ı�,ƥ���ı�)<br>IsMatch(�ı�,ƥ���ı�)<br>  �ж��Ƿ�ƥ�䡣</td> <td></td>
    </tr>
	<tr>
        <td>Guid</td><td>Guid()<br>  ����Guid�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Md5</td><td>Md5(�ı�)<br>Md5(�ı�,��������)<br> ����Md5��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Sha1</td><td>Sha1(�ı�)<br>Sha1(�ı�,��������)<br> ����Sha1��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Sha256</td><td>Sha256(�ı�)<br>Sha256(�ı�,��������)<br> ����Sha256��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Sha512</td><td>Sha512(�ı�)<br>Sha512(�ı�,��������)<br> ����Sha512��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Crc8</td><td>Crc8(�ı�)<br>Crc8(�ı�,��������)<br> ����Crc8��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Crc16</td><td>Crc16(�ı�)<br>Crc16(�ı�,��������)<br> ����Crc16��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Crc32</td><td>Crc32(�ı�)<br>Crc32(�ı�,��������)<br> ����Crc32��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>HmacMd5</td><td>HmacMd5(�ı�,secret)<br>HmacMd5(�ı�,secret,��������)<br> ����HmacMd5��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>HmacSha1</td><td>HmacSha1(�ı�,secret)<br>HmacSha1(�ı�,secret,��������)<br> ����HmacSha1��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>HmacSha256</td><td>HmacSha256(�ı�,secret)<br>HmacSha256(�ı�,secret,��������)<br> ����HmacSha256��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>HmacSha512</td><td>HmacSha512(�ı�,secret)<br>HmacSha512(�ı�,secret,��������)<br> ����HmacSha512��Hash�ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>TrimStart<br>LTrim</td><td>TrimStart(�ı�)<br>LTrim(�ı�)<br>LTrim(�ı�,�ַ���)<br>   �����ַ�����ߡ�</td> <td></td>
    </tr>
	<tr>
        <td>TrimEnd<br>RTrim</td><td>TrimEnd(�ı�)<br>RTrim(�ı�)<br>RTrim(�ı�,�ַ���)<br>   �����ַ����ұߡ�</td> <td></td>
    </tr>
	<tr>
        <td>IndexOf</td><td>IndexOf(�ı�,�����ı�)<br>IndexOf(�ı�,�����ı�,��ʼλ��)<br>IndexOf(�ı�,�����ı�,��ʼλ��,����)<br>   �����ַ���λ�á�</td> <td></td>
    </tr>
	<tr>
        <td>LastIndexOf</td><td>LastIndexOf(�ı�,�����ı�)<br>LastIndexOf(�ı�,�����ı�,��ʼλ��)<br>LastIndexOf(�ı�,�����ı�,��ʼλ��,����)<br>   �����ַ���λ�á�</td> <td></td>
    </tr>
	<tr>
        <td>Split</td><td>Split(�ı�,�ָ���)<br> ��������<br>Split(�ı�,�ָ���,����)<br>  ���طָ������ָ����ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Join</td><td>Join(�ı�1,�ı�2....)<br>  �ϲ��ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>Substring</td><td>Substring(�ı�,λ��)<br>Substring(�ı�,λ��,����)<br>  �и��ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>StartsWith</td><td>StartsWith(�ı�,��ʼ�ı�)<br>StartsWith(�ı�,��ʼ�ı�,�Ƿ���Դ�Сд:1/0)<br>  ȷ�����ַ���ʵ���Ŀ�ͷ�Ƿ���ָ�����ַ���ƥ�䡣</td> <td></td>
    </tr>
	<tr>
        <td>EndsWith</td><td>EndsWith(�ı�,��ʼ�ı�)<br>EndsWith(�ı�,��ʼ�ı�,�Ƿ���Դ�Сд:1/0)<br>  ȷ��ʹ��ָ���ıȽ�ѡ����бȽ�ʱ���ַ���ʵ���Ľ�β�Ƿ���ָ�����ַ���ƥ�䡣</td> <td></td>
    </tr>
	<tr>
        <td>IsNullOrEmpty</td><td>IsNullOrEmpty(�ı�)<br>  ָʾָ�����ַ����� null ���� ���ַ�����</td> <td></td>
    </tr>	
	<tr>
        <td>IsNullOrWhiteSpace</td><td>IsNullOrWhiteSpace(�ı�)<br>  ָʾָ�����ַ����� null���ջ��ǽ��ɿհ��ַ���ɡ�</td> <td></td>
    </tr>
	<tr>
        <td>ToUpper</td><td>ToUpper(�ı�)<br>  ���ı�ת��Ϊ��д��ʽ��</td> <td></td>
    </tr>	
	<tr>
        <td>ToLower</td><td>ToLower(�ı�)<br>  ���ı�ת��ΪСд��ʽ��</td> <td></td>
    </tr>
	<tr>
        <td>RemoveStart</td><td>RemoveStart(�ı�,����ı�)<br>ƥ����ߣ��ɹ���ȥ������ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>RemoveEnd</td><td>RemoveEnd(�ı�,�ұ��ı�)<br>ƥ���ұߣ��ɹ���ȥ���ұ��ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>RemoveBoth</td><td>RemoveBoth(�ı�,����ı�,�ұ��ı�,ͬʱƥ��:0/1(Ĭ��0))<br>ƥ�䷽ʽ, ƥ����ߣ��ɹ���ȥ������ַ�����ƥ���ұߣ��ɹ���ȥ���ұ��ַ�����</td> <td></td>
    </tr>
	<tr>
        <td>P<br>param</td><td>P(�ı�)<br>��̬��ѯ������</td> <td></td>
    </tr>
</table>