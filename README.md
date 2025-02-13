# Abdullahi-repository 
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class CalculatorApp {
    private JFrame frame;
    private JTextField textField;
    private String operator = "";
    private double num1 = 0, num2 = 0, result = 0;

    public CalculatorApp() {
        frame = new JFrame("Calculator");
        frame.setSize(300, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());

        textField = new JTextField();
        textField.setFont(new Font("Arial", Font.BOLD, 24));
        textField.setHorizontalAlignment(SwingConstants.RIGHT);
        frame.add(textField, BorderLayout.NORTH);

        JPanel buttonPanel = new JPanel();
        buttonPanel.setLayout(new GridLayout(4, 4, 10, 10));

        String[] buttons = {
                "7", "8", "9", "/",
                "4", "5", "6", "*",
                "1", "2", "3", "-",
                "C", "0", "=", "+"
        };

        for (String label : buttons) {
            JButton button = new JButton(label);
            button.setFont(new Font("Arial", Font.BOLD, 20));
            button.addActionListener(new ButtonClickListener());
            buttonPanel.add(button);
        }

        frame.add(buttonPanel, BorderLayout.CENTER);
        frame.setVisible(true);
    }

    private class ButtonClickListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            String command = e.getActionCommand();

            if ("0123456789".contains(command)) {
                textField.setText(textField.getText() + command);
            } else if ("/-*+".contains(command)) {
                operator = command;
                num1 = Double.parseDouble(textField.getText());
                textField.setText("");
            } else if (command.equals("=")) {
                num2 = Double.parseDouble(textField.getText());
                switch (operator) {
                    case "/":
                        result = num1 / num2;
                        break;
                    case "*":
                        result = num1 * num2;
                        break;
                    case "-":
                        result = num1 - num2;
                        break;
                    case "+":
                        result = num1 + num2;
                        break;
                }
                textField.setText(String.valueOf(result));
                operator = "";
            } else if (command.equals("C")) {
                textField.setText("");
                operator = "";
                num1 = num2 = result = 0;
            }
        }
    }

    public static void main(String[] args) {
        new CalculatorApp();
    }
}
