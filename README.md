# Втора лабораториска вежба по Софтверско инженерство
Александар Ристов, бр. на индекс 122093

Група на код:

Control Flow Graph

Цикломатска комплексност

Според CFG кој што го најдов од дадената функција checkCart, цикломатската зависност се наоѓа според бројот на јазли, рабови и компоненти.
Во оваа задача најдов три компоненти, 22 јазли и 26 рабови. Ако сакаме да ја пресметаме комплексноста според формулата би било:
Цикломатска комплексност = 26 - 22 + 2*3 = 4 + 2*3 = 10.

Тест случаи според критериумот Every Branch

Според Every Branch критериум, сите резултати или исходи морат да бидат поминати барем еднаш. Тоа значи дека за повеќе комбинации во 
if како "item.getName() == null || item.getName().length() == 0" може да врати true или false. Со две исходи true или false, every branch критериум
е задоволителен. За секоја комбинација од истиот if ќе го разгледаме примерот во точка 5 како Multiple Condition.
	a)Ќе започнам од првата секвенца:
		if (allItems == null){
            throw new RuntimeException("allItems list can't be null!");
        }
		Ако allItems = null, true ќе биде повикано и ќе имаме RuntimeException
		Ако allItems = 1, false ќе биде повикано и немаме  RuntimeException
	б)
		for (int i = 0; i < allItems.size(); i++){...}
		Ako allItems.size() < i, ќе биде false и нема да се изврши циклусот внатре
		ако allItems.size() > i, ќе биде true, ќе се изврши циклусот
	в)
		if (item.getName() == null || item.getName().length() == 0){}
		Ако item.getName() = null, се враќа true и ќе се изврши item.setName("unknown");
		Ако item.getName() = "asd" и item.getName().length() = 1, се враќа false и нема да се изврши
	г)
		if (item.getBarcode() != null){}
		Ако item.getBarcode() = 1. се извршува внатре
		Ако item.getBarcode() = null, се извршува RuntimeException("No barcode!");
	д) 
		for (int j = 0; j < item.getBarcode().length(); j++){}
		Ако item.getBarcode().length() > j, ќе се изврши циклусот
		Ако item.getBarcode().length() <= j, нема да се изврши
	ѓ)
		if (allowed.indexOf(c) == -1){}
		Ako allowed.indexOf(c) = -1, ќе се изврши RuntimeException
		Ако allowed.indexOf(c) = 1, нема да се изврши RuntimeException
	е)
		 Ако if (item.getDiscount() > 0){}, ќе се изврши sum += item.getPrice()*item.getDiscount();
		 Ако if (item.getDiscount() < 0){}, ќе се изврши sum += item.getPrice();
	Ж)
		Овој е целата проверка бидејќи имаме "И" а не "ИЛИ"
		(item.getPrice() > 300 && item.getDiscount() > 0 && item.getBarcode().charAt(0) == '0'){}
		Ако врати true ќе се изврши sum -= 30;
		Ако врати false нема да се изврши sum -= 30;
	з)
		Ако  if (sum <= payment){}, ќе се изврши return true;
		Ако  if (sum > payment){}, ќе се изврши return false;

 
Тест случаи според критериумот Multiple Condition
Според Multiple Condition критериумот значи дека сите комбинации на влез треба да бидат покриени. Во овој случај имаме три влезни атрибути 
	а. item.getPrice() > 300 
	б. item.getDiscount() > 0 
	в. item.getBarcode().charAt(0) == '0'
	1. Во прв случај сите би вратиле true, (true, true, true)
		во излез би имале sum-=30; што би ја намалило сумата
	2. (false, true, true)
		Ќе нема промена на sum
	3. (true, false, true)
		Ќе нема промена на sum
	4. (true, true, false)
		Ќе нема промена на sum
	5. (false, false, true)
		Ќе нема промена на sum
	6. (false, true, false)
		Ќе нема промена на sum
	7. (true, false, false)
		Ќе нема промена на sum
	8. (false, false, false)
		Ќе нема промена на sum
Од овие тест сценарија заклучуваме дека сите комбинации се проверени и само во една комбинација имаме промена на сумата, што го задоволува Multiple Condition критериумот.
