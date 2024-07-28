import java.util.Scanner;

class ListNode {
    int value;
    ListNode next;
    
    ListNode(int value) {
        this.value = value;
        this.next = null;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        
        ListNode head = null, tail = null;
        for (int i = 0; i < N; i++) {
            int value = scanner.nextInt();
            ListNode newNode = new ListNode(value);
            if (head == null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        
        int K = scanner.nextInt();
        scanner.close();
        
        head = appendLastKToFront(head, N, K);
        
        printList(head);
    }
    
    public static ListNode appendLastKToFront(ListNode head, int N, int K) {
        if (head == null || K == 0 || K == N) {
            return head;
        }
        
        // Normalize K to be within the range of the list length
        K = K % N;
        if (K == 0) {
            return head;
        }
        
        ListNode newTail = head;
        for (int i = 0; i < N - K - 1; i++) {
            newTail = newTail.next;
        }
        
        ListNode newHead = newTail.next;
        newTail.next = null;
        
        ListNode temp = newHead;
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = head;
        
        return newHead;
    }
    
    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.value + " ");
            current = current.next;
        }
        System.out.println();
    }
}
