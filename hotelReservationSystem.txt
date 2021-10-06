/**
* The Hotel Reservation Software implements an application that
* simply schedule the booking for Hotel.
*
* @author  Zulfiqar Ibrahim
* @version 1.0
* @since   2021-10-5 
*/











import java.util.Scanner;
import java.util.AbstractMap.SimpleImmutableEntry;
import java.util.ArrayList;
import java.util.List;
import java.util.HashMap;




public class HotelReservationSoftware {

    int size;
    int roomOne;
    int roomTwo;
    int roomThree;
    HashMap<Integer,List<Integer>> roomAndDateRecord=new HashMap<Integer,List<Integer>>();
    List<Integer> valuesRoom1 = new ArrayList<Integer>();
    List<Integer> valuesRoom2 = new ArrayList<Integer>();
    List<Integer> valuesRoom3 = new ArrayList<Integer>();


    public HotelReservationSoftware(){
        // Constructor to intialiye some variables t.
        size = 1000;
        roomOne = 1;
        roomTwo = 2;
        roomThree = 3;



    }
    public void printAllRoomsAndReservation()
    {
        // Prints Booking Reservation Table.
        int line = 0;
        
        Scanner sc = new Scanner(System.in);

        while(true)
        {
            System.out.println(" ");
            System.out.println("Hotel Reservation Booking Information");
            System.out.println(" ");
            System.out.println("Availabe Rooms               Booking Dates");
            System.out.println(" ");
            if(roomAndDateRecord.size() > 0){
                //System.out.println(roomAndDateRecord);
                for (int i : roomAndDateRecord.keySet()) {
                    System.out.println("Room " + i + " =                        "+ roomAndDateRecord.get(i));
                    
                  }
                  System.out.println("--------------------------------");
    
            }
            else{
                
                System.out.println("--------------------------------");
                System.out.println("There are no rooms reserved");
            }
            System.out.println("--------------------------------");
            System.out.print("Press 9 to Go-back to Main Menue:");
            line = sc.nextInt();
            if (line == 9){
            
                break;
            }
            
        }

        //selection.close();
        //mainMenue();

    }
    public void errorGenerationAndStoreInput(int check, int selectRoom, int selectStartDate, int selectEndDate,List<Integer> valuesRoom1,List<Integer> valuesRoom2,List<Integer> valuesRoom3){

        // This fucntion is used to get the corresponding error and according to that error, perform necessarz operation.

        if (check == 0 && (selectRoom == roomOne || selectRoom == roomTwo || selectRoom == roomThree )){

            if (selectStartDate > selectEndDate){
                System.out.println("Date("+selectStartDate+","+selectEndDate+") is in Invalid Formate");
            }
            else if (selectStartDate < 0 || selectEndDate < 0){
                System.out.println("Date("+selectStartDate+","+selectEndDate+") is in Invalid Formate");
            }
            else{
                System.out.println("Date("+selectStartDate+","+selectEndDate+") cannot be assigend to Room "+selectRoom);

            }
        }
        else if (check == 1 && selectRoom == 1){

            roomAndDateRecord.put(selectRoom,valuesRoom1);
        }
        else if (check == 1 && selectRoom == 2){

            roomAndDateRecord.put(selectRoom,valuesRoom2);
        }
        else if (check == 1 && selectRoom == 3){

            roomAndDateRecord.put(selectRoom,valuesRoom3);

        }
        else if (check == 2){

            System.out.print("Check is 2");
            
        }
        else{
            System.out.print("Do nothing");
            
        }
        

    }
    public void frontMenueForRoomReservation()
    {
        // Prints Reseravtion System Nicely
        System.out.print("\nRoom Reservation System\n" +
        "--------------------------------------------\n");
    }
    public void frontMeneueForBookingReservation()
    {
        //Prints the Booking Reseravtion Menue
        System.out.print("\nBooking Reservation System\n" +
        "--------------------------------------------\n");

    }
    public int validateBookingInfo(List<Integer> values,int startDate,int endDate)
    {
        //This fucntion is most crucial function that performs important validation on user input
        int index = 0;
        if(values.size()> 2){

            for (int i =0; i< values.size()-3;i++){
               
                if(startDate >= values.get(i) && startDate <= values.get(i+1)){
                    index=values.size()-2;
                    values.remove(index);
                    index = values.size()-1;
                    values.remove(index);
                    return 0;

                }

            }
            return 1;
        }
        else if (values.size() == 2){
            return 1;
            }
        else{
            return 0;
            }
        

    }
    public int checkBookingInfo(int roomNumber,List<Integer> valuesRoom1,List<Integer> valuesRoom2,List<Integer> valuesRoom3,int selectStartDate, int selectEndDate)
    {
        //It performs the intial checks on User Input and return appropriate error
        if (( roomNumber > 0) && (selectStartDate <= selectEndDate) && (selectStartDate >= 0 && selectEndDate >= 0) && (selectStartDate <= 365 && selectEndDate<= 365))
        {
            if (roomNumber == roomOne){

                valuesRoom1.add(selectStartDate);
                valuesRoom1.add(selectEndDate);
                return validateBookingInfo(valuesRoom1, selectStartDate,selectEndDate);
            }
            else if (roomNumber == roomTwo)
            {
                valuesRoom2.add(selectStartDate);
                valuesRoom2.add(selectEndDate);
                return validateBookingInfo(valuesRoom2, selectStartDate,selectEndDate);

            }
            else if (roomNumber == roomThree){
                valuesRoom3.add(selectStartDate);
                valuesRoom3.add(selectEndDate);
                return validateBookingInfo(valuesRoom3, selectStartDate,selectEndDate);

            }
            else{
                return 0;
            }
           
        }
        else{
            return 0;
        }
        

    }
    public void reserveRoomsAndDates(){
        //This fucntion provides menue for Room reservation system

        Scanner sc = new Scanner(System.in);
        int selectRoom;
        int selectStartDate;
        int selectEndDate;

        
        int check=0;
        int exitNumber=0;
        
        while(true)
        {
            frontMenueForRoomReservation();

            System.out.print("Enter the Room Number (1,2,3) :");
            selectRoom=sc.nextInt();  


            System.out.print("Enter Start Date:");
            selectStartDate = sc.nextInt();

            System.out.print("Enter End Date:");
            selectEndDate = sc.nextInt();
            if (selectRoom == roomOne ){
                check = checkBookingInfo(selectRoom, valuesRoom1,valuesRoom2,valuesRoom3, selectStartDate, selectEndDate);

            }
            else if (selectRoom == roomTwo){
                check = checkBookingInfo(selectRoom, valuesRoom1,valuesRoom2,valuesRoom3, selectStartDate, selectEndDate);

            }
            else if (selectRoom == roomThree){
                check = checkBookingInfo(selectRoom, valuesRoom1,valuesRoom2,valuesRoom3, selectStartDate, selectEndDate);
            }
            else{
                System.out.println("***Sorry, this Room "+selectRoom+" is not availabe in our Hotel***");
            }
            errorGenerationAndStoreInput(check, selectRoom, selectStartDate, selectEndDate,valuesRoom1,valuesRoom2,valuesRoom3);

            System.out.print("Press 9 to Exit and 5 to Continue: ");
            exitNumber = sc.nextInt();

            if (exitNumber == 9){

                break;
                
            }
            else if (exitNumber == 5){
                continue;
            }

        }
        




    }
    public int returnSize(int selectStartDate,int selectEndDate)
    {
        int size = 0;
        for (int i = selectStartDate; i <= selectEndDate; i++ )
        {
            size = size + 1; 

        }
        if (size>=0){
            
            return size;
        }
        else{
            return -1;
        }
    }
    public void reserveBooking(){
        //This fucntuon is used for reserved booking withou any mention of rooms
        Scanner sc = new Scanner(System.in);
        int selectRoom;
        int selectStartDate;
        int selectEndDate;
        int check;
        int size;
        int exitNumber;
        boolean availabilityCheck;
        while(true)
        {
            frontMeneueForBookingReservation();
            availabilityCheck=true;

            System.out.print("Enter Start Date:");
            selectStartDate = sc.nextInt();

            System.out.print("Enter End Date:");
            selectEndDate = sc.nextInt();
            size=returnSize(selectStartDate, selectEndDate);


            if (roomAndDateRecord.size()==0 && size >= 0)
            {
                System.out.println("All three Rooms are alailable ");
                selectRoom = roomOne;
                System.out.println("Room "+ selectRoom+ " is selected");
                check = checkBookingInfo(selectRoom, valuesRoom1,valuesRoom2,valuesRoom3, selectStartDate, selectEndDate);
                errorGenerationAndStoreInput(check, selectRoom, selectStartDate, selectEndDate,valuesRoom1,valuesRoom2,valuesRoom3);
                

            }
            else if (roomAndDateRecord.size() != 0&&  size>=0){
                List<Integer> keyset = new ArrayList<Integer>();
                keyset.add(roomOne);
                keyset.add(roomTwo);
                keyset.add(roomThree);

                for (int k : keyset){
                    check = checkBookingInfo(k, valuesRoom1,valuesRoom2,valuesRoom3, selectStartDate, selectEndDate);
                    if (check == 1 && availabilityCheck)
                    {
                        errorGenerationAndStoreInput(check, k, selectStartDate, selectEndDate,valuesRoom1,valuesRoom2,valuesRoom3);
                        availabilityCheck=false;
                        break;
                    }
                    else{

                        System.out.println("Date("+selectStartDate+","+selectEndDate+") cannot be assigend to Room "+k);;
                    }
                   
                   
                }

                


            }



            System.out.print("Press 9 to Exit and 5 to Continue: ");
            exitNumber = sc.nextInt();

            if (exitNumber == 9){

                break;
                
            }
            else if (exitNumber == 5){
                continue;
            }
        }

    }
    
    public static int mainMenue(){
        int selection;
        Scanner sc = new Scanner(System.in);
        System.out.println("\nHotel Reservation System\n");
        System.out.println("----------------------------\n");
        System.out.println("1. Print all Rooms and Reservation\n");
        System.out.println("2. Reserver a Room(1,2,3)\n");
        System.out.println("3. Reserver a Booking\n");
        System.out.println("4. Exit\n");

        System.out.print("Your selected option is :");
        selection = sc.nextInt();
        System.out.print(" ");
        //sc.close();
        return selection;


    }


    

public static void main(String[] args) {
    HotelReservationSoftware obj1 = new HotelReservationSoftware();
    int userSelected = 0;
    boolean check = true;
    
        
    while(check){

        userSelected = mainMenue();
         
        switch(userSelected){

            case 1:
            obj1.printAllRoomsAndReservation();
            break;

            case 2:
            obj1.reserveRoomsAndDates();
            break;

            case 3:
            obj1.reserveBooking();
            break;

            case 4:
            System.out.print("Exiting the Program...");
            check = false;


            default:
            break;

        }
    }

    
}
}
    

