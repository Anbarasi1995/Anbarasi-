# Anbarasi-
R program colibrary(ggplot2)

weeks <- c(1, 2, 3, 4, 5, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42)

Sleep_Latency <- c(10, 2, 0, 6, 3, 1, 9, 0, 0, 1, 0, 6, 2, 0, 3, 3, 6, 4, 3, 2, 0, 8, 1, 0)
Phase <- rep(c('(A) Baseline', '(B) Intervention', '(C) Washout', '(D) Follow-up'), each = 6)

Sleep_Latency_data <- data.frame(
  Weeks = weeks,
  Sleep_Latency = Sleep_Latency,
  Phase = factor(Phase, levels = c('(A) Baseline', '(B) Intervention', '(C) Washout', '(D) Follow-up'))
)

phase_labels <- c("A", "B", "C", "D")
phase_midpoints <- c(2.5, 12.5, 25, 37)

# Create the ggplot object and assign it to 'sleep_latency_plot'
sleep_latency_plot <- ggplot(Sleep_Latency_data, aes(x = Weeks, y = Sleep_Latency, color = Phase)) +
  geom_vline(xintercept = c(6,19,31), linetype = "dashed", color = "black") +
  geom_line(linewidth = 0.8) +
  geom_point(size = 2.5) +
  geom_smooth(aes(color = Phase, linetype = Phase), method = "lm", se = FALSE, size = 0.5, color = "black") +
  scale_color_manual(values = c("#E9967A", "#E9967A", "#E9967A", "#E9967A")) +
  scale_linetype_manual(values = c('(A) Baseline' = "solid", '(B) Intervention' = "solid", '(C) Washout' = "solid", '(D) Follow-up' = "solid")) +
  scale_x_continuous(breaks = seq(0, 45, 5), limits = c(-2.5, 45), expand = c(0, 0)) +
  scale_y_continuous(breaks = seq(0, 35, 5), limits = c(0, 35), expand = c(0, 0)) +
  labs(title = "Participant 2 - Actigraphy Sleep Latency ",
       x = "Phase-wise Time Points (Weeks)",
       y = "Sleep Latency in Minutes") +
  theme_minimal() +
  theme(
    legend.position = "bottom",
    plot.title = element_text(hjust = 0.5, family = "serif", face = "bold", size = 12),
    axis.title = element_text(family = "serif", size = 12),
    axis.text = element_text(family = "serif", size = 12),
    legend.title = element_blank()
  ) +
  geom_text(data = data.frame(x = phase_midpoints, y = c(30, 30, 30,30), label = phase_labels),
            aes(x = x, y = y, label = label),
            inherit.aes = FALSE,
            family = "serif",
            size = 4,
            color = "black")


tiff("Sleep_Latency_plot.tiff", units = "in", width = 8, height = 6, res = 1200)
print(sleep_latency_plot)
dev.off()
de
