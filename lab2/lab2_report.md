<p>University: <a href="https://itmo.ru/ru/">ITMO University</a></p>

<p>Faculty: <a href="https://fict.itmo.ru">FICT</a></p>

<p>Course: <a href="https://github.com/itmo-ict-faculty/introduction-in-routing">Introduction in routing</a></p>

<p>Year: 2022/2023</p>

<p>Group: K33212</p>

<p>Author: Potitova Valentina Alexandrovna</p>

<p>Lab: Lab2</p>

<p>Date of create: 27.11.2022</p>

<p>Date of finished: 02.12.2022</p>



<h1>����������� ������ �2</h1>

<h2>�������� �������������� ������������� ���� �����, ��������� ����������� ������������� ����� ���������</h2>


<h3>���� ������</h3>

<p>������������ � ���������� ������������ IP �������, ��������� ����������� ������������� � �������� ��������� ���������.</p>


<h3>���������� ������</h3>

<ul>

<li>����, ������� ������������� ��� ������������� �������� ���� ��������� � ����� � ������������ �������. ��� �����: "lab2.yaml".</li>
</ul>

<h4>C���� �����</h4>
<img src="�����.jpg" alt="C���� �����">

<h4>����� ������������ ��� ������� �������� ����������</h4>
<h5> R01.MSK (sudo ssh admin@172.20.20.8)</h5>
<pre><code>
/ip pool
add name=pool1 ranges=192.168.10.10-192.168.10.254
/ip dhcp-server
add address-pool=pool1 disabled=no interface=ether4 name=dhcp1
/ip address
add address=172.15.255.30/30 interface=ether1 network=172.15.255.28
add address=10.10.1.1/30 interface=ether2 network=10.10.1.0
add address=10.10.2.1/30 interface=ether3 network=10.10.2.0
add address=192.168.10.1/24 interface=ether4 network=192.168.10.0
/ip dhcp-client
add disabled=no interface=ether1
/ip route
add distance=1 dst-address=192.168.20.0/24 gateway=10.10.2.2
add distance=1 dst-address=192.168.30.0/24 gateway=10.10.1.2
/system identity
set name=R01.MSK
</code></pre>

<h5>R01.FRT (sudo ssh admin@172.20.20.9)</h5>
<pre><code>
/ip pool
add name=pool2 ranges=192.168.20.10-192.168.20.254
/ip dhcp-server
add address-pool=pool2 disabled=no interface=ether4 name=dhcp2
/ip address
add address=172.15.255.30/30 interface=ether1 network=172.15.255.28
add address=10.10.2.2/30 interface=ether3 network=10.10.2.0
add address=10.10.3.1/30 interface=ether2 network=10.10.3.0
add address=192.168.20.1/24 interface=ether4 network=192.168.20.0
/ip dhcp-client
add disabled=no interface=ether1
/ip route
add distance=1 dst-address=192.168.10.0/24 gateway=10.10.2.1
add distance=1 dst-address=192.168.30.0/24 gateway=10.10.3.2
/system identity
set name=R01.FRT
</pre></code>

<h5>R01.BRL (sudo ssh admin@172.20.20.7)</h5>
<pre><code>
/ip pool
add name=pool3 ranges=192.168.30.10-192.168.30.254
/ip dhcp-server
add address-pool=pool3 disabled=no interface=ether4 name=dhcp3
/ip address
add address=172.15.255.30/30 interface=ether1 network=172.15.255.28
add address=10.10.1.2/30 interface=ether2 network=10.10.1.0
add address=10.10.3.2/30 interface=ether3 network=10.10.3.0
add address=192.168.30.1/24 interface=ether4 network=192.168.30.0
/ip dhcp-client
add disabled=no interface=ether1
/ip route
add distance=1 dst-address=192.168.10.0/24 gateway=10.10.1.1
add distance=1 dst-address=192.168.20.0/24 gateway=10.10.3.1
/system identity
set name=R01.BRL
</pre></code>

<h5>PC1 (sudo ssh admin@172.20.20.3)</h5>
<pre><code>
/ip address
add address=172.15.255.30/30 interface=ether1 network=172.15.255.28
/ip dhcp-client
add disabled=no interface=ether1
add disabled=no interface=ether2
/ip route
add distance=1 dst-address=10.10.1.0/30 gateway=192.168.10.1
add distance=1 dst-address=10.10.2.0/30 gateway=192.168.10.1
add distance=1 dst-address=192.168.20.0/24 gateway=192.168.10.1
add distance=1 dst-address=192.168.30.0/24 gateway=192.168.10.1
/system identity
set name=PC1
</pre></code>

<h5>PC2 (sudo ssh admin@172.20.20.5)</h5>
<pre><code>
/ip address
add address=172.15.255.30/30 interface=ether1 network=172.15.255.28
/ip dhcp-client
add disabled=no interface=ether1
add disabled=no interface=ether2
/ip route
add distance=1 dst-address=10.10.2.0/30 gateway=192.168.20.1
add distance=1 dst-address=10.10.3.0/30 gateway=192.168.20.1
add distance=1 dst-address=192.168.10.0/24 gateway=192.168.20.1
add distance=1 dst-address=192.168.30.0/24 gateway=192.168.20.1
/system identity
set name=PC2
</pre></code>

<h5>PC3 (sudo ssh admin@172.20.20.4)</h5>
<pre><code>
/ip address
add address=172.15.255.30/30 interface=ether1 network=172.15.255.28
/ip dhcp-client
add disabled=no interface=ether1
add disabled=no interface=ether2
/ip route
add distance=1 dst-address=10.10.1.0/30 gateway=192.168.30.1
add distance=1 dst-address=10.10.3.0/30 gateway=192.168.30.1
add distance=1 dst-address=192.168.10.0/24 gateway=192.168.30.1
add distance=1 dst-address=192.168.20.0/24 gateway=192.168.30.1
/system identity
set name=PC3
</pre></code>

<h4>���������� ������, �������� ��������� ���������</h4>
<p></p>
<img src="1.png" alt="����� ip-�������">
<p></p>
<img src="2.png" alt="����������� ������">
<p></p>
<img src="3.png" alt="ip-����� ����������">

<h3>�����</h3>
<p></p>