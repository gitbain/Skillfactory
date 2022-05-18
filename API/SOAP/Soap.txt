Post/Order HTTP/1.1
Host: www.mamamiapizzeria.com
Content-Type:application/soap+xml;charset=utf-8
Content-Length: nnn

<<?xml version='1.0' encoding="UTF-8"?>>
    <Body>
        <addOrder>
		    <addOrderRequest>
                <PizzaName>Пепперони</PizzaName>
			    <PizzaSize>Средняя<PizzaSize>
                <PizzaSizeCm>35см</PizzaSizeCm>
                <PizzaTopping>Бекон</PizzaTopping>
			    <ToppingAmount>1</ToppingAmount>
				<OrderDate>2022-02-21</OrderDate>
				<OrderCost>600 рублей</OrderCost>
			</addOrderRequest>
        </addOrder>
    </Body>


Response
HTTP/1.1 200OK
Content-Type:application/soap+xml;charset=utf-8
Content-Length: nnn

<?xml version='1.0' encoding='UTF-8'?>
<env:Envelope xmlns:env="http://www.w3.org/2003/05/soap-envelope">
    <env:Body>
        <addOrder>
		    <addOrderResponse>
                <OrderId>555</OrderId>
			</addOrderResponse>
        </addOrder>
    </env:Body>
</env:Envelope>

Fault
HTTP/1.1 422Error
Content-Type:application/soap+xml;charset=utf-8
Content-Length: nnn

<?xml version='1.0' encoding='UTF-8'?>
<env:Envelope xmlns:env="http://www.w3.org/2003/05/soap-envelope">
    <env:Body>
        <env:Fault>
		    <FaultResponse>
                <ErrorCode>422</ErrorCode>
				<ErrorMessage>Unprocessable Entity</ErrorMessage>
			</FaultResponse>
        </env:Fault>
    </env:Body>
</env:Envelope>



XDS schema
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
<xs:element name="Order">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="PizzaName" type="xs:string"/>
            <xs:element name="PizzaSize" type="xs:string"/>
			    <xs:simpleType>
				    <xs:restriction base="xs:string">
					    <xs:enumeration value="Маленькая"/>
						<xs:enumeration value="Средняя"/>
						<xs:enumeration value="Большая"/>
				    </xs:restriction>
				</xs:simpleType>
			</xs:element>
			<xs:element name="PizzaSizeCm" type="xs:integer"/>
 	            <xs:simpleType>
    	            <xs:restriction base="xs:integer">
         	            <xs:minInclusive value="25"/>
					    <xs:maxInclusive value="35"/>
     	            </xs:restriction>
	            </xs:simpleType>
            </xs:element>
			<xs:element name="PizzaTopping" type="xs:string"/>
			    <xs:simpleType>
				    <xs:restriction base="xs:string">
					    <xs:enumeration value="Бекон"/>
						<xs:enumeration value="Курица"/>
						<xs:enumeration value="Помидоры"/>
						<xs:enumeration value="Сыр"/>
						<xs:enumeration value="Лук"/>
				    </xs:restriction>
				</xs:simpleType>
			</xs:element>		   
		    <xs:element name="ToppingAmount" type="xs:integer"/>
 	            <xs:simpleType>
    	            <xs:restriction base="xs:integer">
         	            <xs:minInclusive value="1"/>
					    <xs:maxInclusive value="5"/>
     	            </xs:restriction>
	            </xs:simpleType>
            </xs:element>
			<xs:element name="OrderDate" type="xs:date"/>
			<xs:element name="OrderCost" type="xs:integer"/>
        </xs:sequence>
      <xs:attribute name="lang" type="xs:string" default="RU"/>
    </xs:complexType>
</xs:element>
</xs:schema>

<Order lang="RU">
<Order/>
