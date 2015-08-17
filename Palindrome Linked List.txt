/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

/**
 * Given a singly linked list, determine if it is a palindrome.
 * Follow up:
 * Could you do it in O(n) time and O(1) space?
 * Yes, as folows.
 */

public class Solution {
    public boolean isPalindrome(ListNode head) {
        // Find out number of nodes.
        int length = 0;
        ListNode current = head;
        while (current != null) {
            current = current.next;
            length += 1;
        }
        // Revert the first half nodes
        current = head;
        ListNode previous = null;
        for (int i = 0; i < length/2; i += 1) {
            ListNode tmp = current.next;
            current.next = previous;
            previous = current;
            current = tmp;
        }
        // "previous" is the head of reverted first half,
        // and "current" is the head of second half.
        if (length % 2 == 1 && previous != null) {
            current = current.next;
        }
        // compare the reverted first half and the second half.
        while (previous != null) {
            if (previous.val != current.val) {
                return false;
            }
            previous = previous.next;
            current = current.next;
        }
        return true;
    }
}