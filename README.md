# change the prefix from 'C-b' to 'C-a'
# (remap capslock to CTRL for easy access)
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# start with window 1 (instead of 0)
set -g base-index 1

# start with pane 1
set -g pane-base-index 1

# split panes using | and -, make sure they open in the same path
bind | split-window -h -c "#{pane_current_path}"
bind - split-window -v -c "#{pane_current_path}"

unbind '"'
unbind %

# open new windows in the current path
bind c new-window -c "#{pane_current_path}"

# reload config file
bind r source-file ~/.tmux.conf

unbind p
bind p previous-window

# shorten command delay
set -sg escape-time 1

# don't rename windows automatically
set -g allow-rename off

# mouse control (clickable windows, panes, resizable panes)
set -g mouse on

# Use Alt-arrow keys without prefix key to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# enable vi mode keys
set-window-option -g mode-keys vi

# set default terminal mode to 256 colors
set -g default-terminal "screen-256color"

# present a menu of URLs to open from the visible pane. sweet.
bind u capture-pane \;\
    save-buffer /tmp/tmux-buffer \;\
    split-window -l 10 "urlview /tmp/tmux-buffer"


######################
### DESIGN CHANGES ###
######################

# loud or quiet?
set -g visual-activity off
set -g visual-bell off
set -g visual-silence off
setw -g monitor-activity off
set -g bell-action none

#  modes
setw -g clock-mode-colour colour5
setw -g mode-style 'fg=colour1 bg=colour18 bold'

# panes
set -g pane-border-style 'fg=colour19 bg=colour0'
set -g pane-active-border-style 'bg=colour0 fg=colour5'

# statusbar
set -g status-position bottom
set -g status-justify left
set -g status-style 'bg=colour18 fg=colour4'
set -g status-left ''
set -g status-right '#[fg=colour18,bg=colour4] %d/%m #[fg=colour4,bg=colour18] %H:%M:%S '
set -g status-right-length 50
set -g status-left-length 20

setw -g window-status-current-style 'fg=colour1 bg=colour19 bold'
setw -g window-status-current-format ' #I #[fg=colour7]#W#[fg=colour8]#F '

setw -g window-status-style 'fg=colour1 bg=colour18 dim'
setw -g window-status-format ' #I #[fg=colour250]#W#[fg=colour244]#F '

setw -g window-status-bell-style 'fg=colour255 bg=colour1 bold'

# messages
set -g message-style 'fg=colour18 bg=colour4 bold'

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-battery'
set -g @plugin 'tmux-plugins/tmux-open'
set -g @plugin 'tmux-plugins/tmux-yank'
set -g @plugin 'tmux-plugins/tmux-prefix-highlight'
set -g @plugin 'tmux-plugins/tmux-copycat'

# Disable confirm before killing
bind-key x kill-pane
bind-key X kill-window

# This tmux statusbar config was created by tmuxline.vim
# on Wed, 25 Nov 2015
set -g status "on"
set -g status-bg "colour236" 
set -g status-justify "left"
set -g status-position "top"
set -g status-left-length "100"
set -g status-right-length "100"
set -g status-left "#{prefix_highlight}#[fg=colour22,bg=colour148,bold] #S #[fg=colour148,bg=colour236,nobold,nounderscore,noitalics]"
set -g status-right "#[fg=colour240,bg=colour236,nobold,nounderscore,noitalics]#[fg=colour250,bg=colour240] %Y-%m-%d %H:%M #[fg=colour252,bg=colour240,nobold,nounderscore,noitalics]#[fg=colour241,bg=colour252] #h "

setw -g window-status-separator ""
setw -g window-status-format "#[fg=colour245,bg=colour236] #I #[fg=colour245,bg=colour236]#W "
setw -g window-status-current-format "#[fg=colour236,bg=colour240,nobold,nounderscore,noitalics]#[fg=colour231,bg=colour240] #I #[fg=colour231,bg=colour240]#{?window_zoomed_flag,#[fg=green][],}#W #[fg=colour240,bg=colour236,nobold,nounderscore,noitalics]"
