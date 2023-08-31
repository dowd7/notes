```java
import java.util.*;

class Main {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int noOfPlayers = scan.nextInt();

        List<Player> playersList = new ArrayList<>();
        for (int i = 1; i <= noOfPlayers; i++) {
            Player player = new Player(scan.next(), scan.nextDouble(), scan.next());
            playersList.add(player);
        }

        Map<Integer, Player> finalSetOfPlayers = new HashMap<>();
        finalSetOfPlayers = Player.selectionProcess(playersList, noOfPlayers);
        System.out.println(finalSetOfPlayers);
        scan.close();

    }

}

class Player implements Comparable<Player> {
    private String playerName;
    private Double avarage;
    private String playerDOB;

    public Player(String playerName, Double avarage, String playerDOB) {
        super();
        this.playerName = playerName;
        this.avarage = avarage;
        this.playerDOB = playerDOB;
    }

    public String getPlayerName() {
        return playerName;
    }

    public void setPlayerName(String playerName) {
        this.playerName = playerName;
    }

    public Double getAvarage() {
        return avarage;
    }

    public void setAvarage(Double avarage) {
        this.avarage = avarage;
    }

    public String getPlayerDOB() {
        return playerDOB;
    }

    public void setPlayerDOB(String playerDOB) {
        this.playerDOB = playerDOB;
    }



    @Override
    public String toString() {
        return this.playerName + "";
    }

    //override the compareTo method
    //order is higher average, then higher DOB, then natural order of name
    @Override
    public int compareTo(Player player) {
        if (this.avarage > player.avarage) {
            return -1;
        } else if (this.avarage < player.avarage) {
            return 1;
        } else {
            if (this.playerDOB.compareTo(player.playerDOB) < 0) {
                return -1;
            } else if (this.playerDOB.compareTo(player.playerDOB) > 0) {
                return 1;
            } else {
                return this.playerName.compareTo(player.playerName);
            }
        }
    }


    public static Map<Integer, Player> selectionProcess(List<Player> playerList, int noOfPlayers) {
        //Create a local variable ‘playerSet’, which is a TreeSet and store all the
        // Player objects from playerList, based on the logic provided by overriding the compareTo() method
        //create another local variable ‘finalBattingOrder’, which is HashMap. The key and value pair for
        // this HashMap should be ‘<Integer, Player>’. By using the variable ‘noOfPlayers’ copy all the
        // elements from ‘playerSet’ and put them into the ‘finalBattingOrder’. The batting order
        // should start from 1 instead of 0
        //return the ‘finalBattingOrder’

        Set<Player> playerSet = new TreeSet<>();
        //store all the Player objects from playerList, based on the logic provided by overriding the compareTo() method
        for (Player player : playerList) {
            playerSet.add(player);
        }

        Map<Integer, Player> finalBattingOrder = new HashMap<>();
        int i = 1;
        for (Player player : playerSet) {
            finalBattingOrder.put(i, player);
            i++;
        }
        return finalBattingOrder;

    }
}
```
```java
import java.util.Scanner;

class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int noOfChildren = sc.nextInt();
        String giftStockAvailibility = sc.next();

        //John wants to buy the costliest gifts for all the kids during the Christmas party.
        // The stock availability of gifts in the store and the number of kids are given.
        // Write a program to print the amount required to buy the gifts. Print 0 if
        // enough stock doesn’t exist.
        //
        //Please note John can buy any one of the gifts not a combination of gifts.
        // That means the same gifts have to be given to all the kids

        //First-line contains the number of kids ‘N’ and the second line contains the
        // gift stock availability details ‘S’ in the format giftname:price:quantityavailable
        // separated by a comma.

        //Sample Input 1: 5
        //Chocolate:30:2,IceCream:15:8

        //Print the amount required by John to buy the most expensive gift. Print 0 if there isn’t
        // enough stock(i.e. Quantity Available of each gift < No of Kids)

        String [] giftStock = giftStockAvailibility.split(",");
        String[] gift1 = giftStock[0].split(":");
        String[] gift2 = giftStock[1].split(":");

        int gift1Quantity = Integer.valueOf(gift1[2]);
        int gift1Price = Integer.valueOf(gift1[1]);
        int gift2Price = Integer.valueOf(gift2[1]);
        int gift2Quantity = Integer.valueOf(gift2[2]);

        int gift1TotalPrice = gift1Price * noOfChildren;
        int gift2TotalPrice = gift2Price * noOfChildren;



        if(gift1Quantity >= noOfChildren && gift2Quantity >= noOfChildren){
            if(gift1TotalPrice > gift2TotalPrice){
                System.out.println(gift1TotalPrice);
            }else{
                System.out.println(gift2TotalPrice);
            }
        }else if(gift1Quantity >= noOfChildren){
            System.out.println(gift1TotalPrice);
        }else if(gift2Quantity >= noOfChildren) {
            System.out.println(gift2TotalPrice);
        }else{
            System.out.println(0);
        }

        sc.close();
    }

}
```
```java
import java.util.Scanner;

class Main {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        String PANNo = null;
        String aadharNo = null;
        String personName = scan.nextLine();
        Integer age = scan.nextInt();
        Long mobileNo = scan.nextLong();
        Person person = new Person(personName, age, mobileNo);

        if (validate(person)) {
            PANNo = generatePANNumber(person);
            aadharNo = generateAadharNumber(person);
            System.out.println("Success: Your PAN Number is:" + PANNo + " and Aadhar Number is:" + aadharNo + ".");

        } else {
            System.out.println("Error: Your PAN and Aadhar Number can't be generated.");
        }

        scan.close();

    }

    public static Boolean validate(Person person) {
        //Validate the name of the person as below:
        //It should NOT be empty or just spaces. Single spaces between words are allowed.
        //It must contain alphabets and spaces only.
        //It should have a minimum of one word. If it has more than one word, then there must be a space between each word.
        //The length of each word should be at least 1.
        //Each word should start with an uppercase alphabet. All the other characters should be lowercase alphabets.
        if (person.getName().trim().length() == 0) {
            System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
            return false;
        }
        String[] name = person.getName().split(" ");
        for (String s : name) {
            if (s.length() == 0) {
                System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
                return false;
            }
            if (!s.matches("[a-zA-Z]+")) {
                System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
                return false;
            }
            if (!Character.isUpperCase(s.charAt(0))) {
                System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
                return false;
            }
            for (int i = 1; i < s.length(); i++) {
                if (!Character.isLowerCase(s.charAt(i))) {
                    System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
                    return false;
                }
            }
        }
        //Validate the age of the person as below:
        //Applying for a PAN card and Aadhar card required a minimum age of 18 years and maximum 59 years.
        if (person.getAge() < 18 || person.getAge() > 59) {
            System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
            return false;
        }
        //Validate the mobileNo of the person as below:
        //MobileNo must be a 10-digit number and all the numbers should not be the same.
        String mobileNo = person.getMobileNo().toString();
        if (mobileNo.length() != 10) {
            System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
            return false;
        }
        for (int i = 0; i < mobileNo.length(); i++) {
            if (mobileNo.charAt(i) != mobileNo.charAt(0)) {
                break;
            }
            if (i == mobileNo.length() - 1) {
                System.out.println("Error: Provided Name/Age/MobileNo is Invalid.");
                return false;
            }
        }
        return true;



    }

    public static String generatePANNumber(Person person) {
        //This method returns the PAN number of the person. The length of the PAN number must be 10.
        //First, remove all the white spaces in the person’s name.
        //If the person’s name containing a minimum of 6 characters then the PAN number will be the first 5 letters of
        // the person's name in Caps, followed by the age twice, followed by the 6th character of the person's name in Caps.
        // (For example, if the person’s name is ‘Sherlok’ and the person’s age is “27”, then the PAN number will be “SHERL2727O”).
        //Else, if the person’s name containing less than 6 characters then the PAN number will be the person's name in Caps,
        // followed by the required number of ‘A’s, followed by the age twice, followed by a “Z”.(For example,
        // if the person’s name is ‘Tom’ and the person’s age is “27”, then the PAN number will be “TOMAA2727Z”,
        // another example if the person’s name is ‘John and the person’s age is “27”, then the PAN number will be “JOHNA2727Z”).
        //Return the PAN Number.

        String name = person.getName().replaceAll("\\s", "");
        int length = name.length();
        int age = person.getAge();
        if (name.length() >= 6) {

            return name.substring(0,5).toUpperCase() + age + age + Character.toUpperCase(name.charAt(5));
        } else {
            String as = "";
            for(int i = 0; i < 5 - length; i++) {
                as += "A";
            }
            return name.toUpperCase() + as + age + age + "Z";
        }

    }

    public static String generateAadharNumber(Person person) {
        //This method returns the Aadhar number of the person. The format of the Aadhar number must be XXXX XXXX XXXX,
        // where ‘X’ represents a digit.
        //The Aadhar Number should start with 1234, followed by a space, followed by age twice, followed by a space,
        // followed by 9876. (For example, if the person’s age is “27”, then the Aadhar number will be “1234 2727 9876”,
        // another example if the person’s age is “42”, then the PAN number will be “1234 4242 9876”).
        //Return the Aadhar Number.

        return "1234 " + person.getAge().toString() + person.getAge().toString() + " 9876";



    }

}

class Person {
    private String name;
    private Integer age;
    private Long mobileNo;

    public Person(String name, Integer age, Long mobileNo) {
        super();
        this.name = name;
        this.age = age;
        this.mobileNo = mobileNo;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public Long getMobileNo() {
        return mobileNo;
    }

    public void setMobileNo(Long mobileNo) {
        this.mobileNo = mobileNo;
    }

}
```
