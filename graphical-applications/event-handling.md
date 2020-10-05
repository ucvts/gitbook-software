# Event Handling

{% hint style="info" %}
* _Core Java: Volume I—Fundamentals_
  * 10, 11, and 12
* [Trail: Creating a GUI with JFC/Swing](https://docs.oracle.com/javase/tutorial/uiswing/index.html)
{% endhint %}

## Listeners

You'll likely spend a lot of time laying out your components inside of panels and frames. If you're a perfectionist like me, you'll want everything exactly in its place. That's all well and good, but looks aren't everything. Our users are going to want to interact with our interfaces. There are a number of listeners that allow our GUI components to respond to certain actions a user might take.

## Action Listeners

An action listener is one of the most common event handlers you'll need to implement. We use action listeners to define how our program should respond when a user performs an action, such as clicking a button, choosing a menu item, or selection a checkbox or radio button.

Whenever the user performs an action, Java sends out what is called an `actionPerformed` message. Any action listeners registered with the component can then respond to the action. Let's use a simple button click as an example.

```java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

/**
 * Our ActionDemo class implements the ActionListener interface.
 * There's just one method in the ActionListener interface, and
 * it's called actionPerformed. It responds to actions the user
 * takes on our GUI components. Since we're implementing this
 * interface, it's our job to implement this method.
 */
 
public class ActionDemo implements ActionListener {
    
    private int clicks;        // tracks the number of clicks
    private JButton button;    // button triggers updates to clicks
    private JLabel label;      // label displays clicks
    
    /**
     * Creates an instance of the ActionDemo class, initially
     * setting clicks to 0.
     */
     
    public ActionDemo() {
        this.clicks = 0;
    }
    
    /**
     * It's bad practice to do all our GUI initialization in the
     * main method, so we move it to a separate instance method.
     */
     
    public void createAndShowGui() {
        JFrame frame = new JFrame("My Frame");    // create frame
        JPanel panel = new JPanel();              // create panel
        button = new JButton("Click Me");         // create button
        
        // create label with an initial text value of 0, which
        // is derived from the value of clicks
        
        label = new JLabel(String.valueOf(clicks));
        
        // this is an important part: registering the action listener.
        // we pass in this (which refers to this class) because this
        // class is implementing (and therefore acting as) the
        // action listener. when the button is clicked, the
        // actionPerformed method in this class will be called.
        
        button.addActionListener(this);
        
        panel.add(button);    // add button to panel
        panel.add(label);     // add label to panel
        
        frame.add(panel);            // add panel to frame
        frame.setSize(400, 200);     // set frame size
        frame.setVisible(true);      // show frame
    }

    /**
     * This method will be called when the button is clicked.
     */
     
    @Override
    public void actionPerformed(ActionEvent e) {
    
        // first, we get the source of the action. in this example,
        // this is redudant. the only possibly source component is
        // our button. however, in a class with more than one button,
        // this is how we'd determine which button was clicked.
        
        Object source = e.getSource();
        
        // if the source is equal to our button, then we update the label.
        
        if (source.equals(button)) {            
            label.setText(String.valueOf(++clicks));    // update label
        }
        
        // remember, if we have more than one button, we need to be
        // able to determine which button was clicked. for example:
        //
        // if (source.equals(firstButton)) {
        //     labelOne.setText("blah");
        // } else if (source.equals(secondButton)) {
        //     labelTwo.setText("blah blah");
        // }
    }
    
    /**
     * As always, our main method kicks of program execution.
     */
     
    public static void main(String[] args) {
        new ActionDemo().createAndShowGui();
        
        // we only need an ActionDemo object to call the
        // createAndShowGui method. this is the shorthand
        // equivalent of doing this:
        //
        // ActionDemo demo = new ActionDemo(); 
        // demo.createAndShowGui();
    }
}

```

This is a pretty simple program. It's got a `JLabel` and `JButton`, and clicking the `JButton` updates the text of the `JLabel`. I've commented this program thoroughly to help you follow along with what I'm doing and why. Here's what it would look like after it was launched and the user clicked the button twice.

![](../.gitbook/assets/actionlistener.png)

Check out [the Java Tutorials](https://docs.oracle.com/javase/tutorial/uiswing/events/actionlistener.html) for even more on action listeners.

## Mouse Listeners

TODO

## Key Listeners

TODO

```java
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

/**
 * Our KeyDemo class implements the KeyListener interface. There
 * are three methods in the KeyListener interface, and they're
 * called keyTyped, keyPressed, and keyReleased. They respond to
 * various phases of the user hitting a key on the keyboard.
 * Since we're implementing this interface, it's our job to
 * implement these methods.
 */
 
public class KeyDemo implements KeyListener {
    
    private JLabel label;
    
    /**
     * It's bad practice to do all our GUI initialization in the
     * main method, so we move it to a separate instance method.
     */
     
    public void createAndShowGui() {
        JFrame frame = new JFrame("My Frame");    // create frame
        JPanel panel = new JPanel();              // create panel
        
        // create label with an initial text value of Key Pressed.
        // when the user types keys later, this text will change
        // accordingly.
        
        label = new JLabel("Key Pressed: ");
        
        // this is an important part: registering the key listener.
        // we pass in this (which refers to this class) because this
        // class is implementing (and therefore acting as) the
        // key listener. when the button is clicked, the associated
        // key listener methods in this class will be called.
        
        frame.addKeyListener(this);
        
        panel.add(label);    // add label to panel
        
        frame.add(panel);            // add panel to frame
        frame.setSize(400, 200);     // set frame size
        frame.setVisible(true);      // show frame
    }
    
    /**
     * Called immediately after a user types a Unicode character.
     */
    
    @Override
    public void keyTyped(KeyEvent e) {
        label.setText("Key Pressed: " + e.getKeyChar());    // upate label
    }

    /**
     * Called immediately after a user pressed a key down.
     */
    
    @Override
    public void keyPressed(KeyEvent e) {
    
        // we're not actually doing this, but here's an example of
        // when we might use this over the keyTyped method.
        
        if (e.getKeyCode() == KeyEvent.VK_SHIFT) {
            // the Shift button doesn't have a Unicode value, so
            // just pressing the Shift button won't be picked up
            // by the keyTyped method. we can respond to this
            // (and other special keys) in this method.
        }
    }

    /**
     * Called immediately after a user releases a previously pressed key.
     */
    
    @Override
    public void keyReleased(KeyEvent e) {
        // unimplemented, but there might be unique cases where
        // you specifically need to wait for a user to release a
        // a key to do something. maybe you're making a game
        // where something happens while a certain key is pressed,
        // and that something needs to stop happening whenever
        // the key is released.
    }
    
    /**
     * As always, our main method kicks of program execution.
     */
     
    public static void main(String[] args) {
        new KeyDemo().createAndShowGui();
    }
}

```

TODO

![](../.gitbook/assets/keylistener.png)

Check out [the Java Tutorials](https://docs.oracle.com/javase/tutorial/uiswing/events/keylistener.html) for even more on key listeners.

