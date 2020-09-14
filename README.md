//Shashank Eeda
import java.util.*;
import java.util.ArrayList;
import java.util.List;
public class SortColumns {
    /*
    The method minDeletionSize will return -1 in the list if all the strings in the array are not of the same
    length, otherwise it will check the each index of every string in the array and if it is not in order
    it will store the index in the List and then keep checking the next index.
     */
    public List<Integer> minDeletionSize(String [] A){
        ArrayList<Integer> indexes=new ArrayList<Integer>();
        for(int i=0;i<A.length;i++){
            int len=A[0].length();
            if(A[i].length()==len)
                continue;
            else {
                indexes.add(-1);
                return indexes;
            }
        }
        for(int i=0;i<A.length;i++){
            for(int j=0;j<A[0].length()-1;j++){
                if(A[j].charAt(i)<=A[j+1].charAt(i)){
                    continue;
                }
                else{
                    indexes.add(i);
                    break;
                }
            }
        }
        return indexes;
    }
    /*
    postArray will print the array before the strings are modified
     */
    public void postArray(String[] arr){
        for(int i=0;i<arr.length;i++)
            System.out.print(arr[i]+" ");
    }
    /*
    afterArray will print the array after the string indexes are deleted
     */
    public void afterArray(String[] arr,List<Integer> index){
        for(int i=0;i<arr.length;i++){
            for(int j=0;j<arr[0].length();j++){
                if(index.contains(j))
                    continue;
                else{
                    System.out.print(arr[i].charAt(j));
                }
            }
            System.out.print(" ");
        }
    }
    public static void main(String[] args){
        SortColumns tester=new SortColumns();
        List<Integer> removedindexes=new ArrayList<Integer>();
        int n;
        Scanner input = new Scanner(System.in);
        int index=0;
        int acc=0;
        boolean truth=true;
        /*
        This is where the user will be allowed to choose how many strings he/she would like to enter
         */
        System.out.println("How many strings will you enter");
        n=input.nextInt();
        String[] arr=new String[n];
        /*
        This is where the user will input the strings
         */
        for(int i=0;i<n;i++){
            System.out.println("Enter a String");
            arr[i]=input.next();
        }
        /*
        This is where the users input will be printed out
         */
        System.out.print("Original Array: ");
        tester.postArray(arr);
        System.out.println();
        /*
        removedindexes will recieve the indexes that should be deleted in the form of a List
         */
        removedindexes=tester.minDeletionSize(arr);
        /*
        If the size is 0, either nothing was inputted or everything was in order so a message saying all
        columns are in order will be printed
         */
        if(removedindexes.size()==0){
            System.out.println("All the columns are sorted in order");
            System.out.println(removedindexes);
        }
        /*
        This while loop will first check if there is a -1 in the index, if so then an error will be printed
        saying there are unequal lengths and exit the loop. Otherwise it will print the the columns and
        the letters which are not sorted in order
         */
        while(acc<removedindexes.size()) {
            int i=removedindexes.get(index);
            if (removedindexes.get(0) == -1) {
                System.out.println("The rows contain columns of unequal length, which is not allowed according to the description\n" +
                        "above.");
                System.out.println(removedindexes);
                truth=false;
                break;
            }
            if (acc == 0) {
                System.out.print("D=" + removedindexes + " ");
                System.out.println("or D=" + removedindexes.size());
            }

            System.out.print("Column " + i + ": ");
            for (int j = 0; j < arr.length; j++) {
                System.out.print("\"" + arr[j].charAt(i) + "\" ");
            }
            System.out.print("is not sorted");
            System.out.println();
            index++;
            acc++;
            }
        /*
        This will post the array after it was modified
         */
        if(truth==true) {
            System.out.print("After Array: ");
            tester.afterArray(arr, removedindexes);
        }
    }
    /*
    Sample input and output:

    How many strings will you enter
    3
    Enter a String
    aza
    Enter a String
    bvb
    Enter a String
    cac
    Original Array: aza bvb cac
    D=[1] or D=1
    Column 1: "z" "v" "a" is not sorted
    After Array: aa bb cc
     */
}
