# SimpleABCViewer

fork from alembic-1.5.8.

build with alembic-1.7.1 on Windows10(64bit).

# Usage

```
> SimpleABCViewer.exe -f alembic_octopus.abc 
```

# Mouse

``alt + drag``

# Keyboard

```c
void keyboard( unsigned char key, int x, int y )
{
    static bool bf = true;

    switch ( key )
    {
    case '`':
    case '~':
        glutFullScreen();
        break;
    case 'f':
    case 'F':
        g_state.scene.cam.frame( g_transport->getBounds() );
        g_state.scene.cam.autoSetClippingPlanes( g_transport->getBounds() );
        glutPostRedisplay();
        break;
    case 'c':
        TickBackward();
        break;
    case 'v':
        TickForward();
        break;

    case '>':
    case '.':
        if ( g_state.playback == kForward )
        {
            g_state.playback = kStopped;
            glutIdleFunc( NULL );
        }
        else
        {
            g_state.playback = kForward;
            glutIdleFunc( playFwdIdle );
        }
        break;
    case '<':
    case ',':
        if ( g_state.playback == kBackward )
        {
            g_state.playback = kStopped;
            glutIdleFunc( NULL );
        }
        else
        {
            g_state.playback = kBackward;
            glutIdleFunc( playBwdIdle );
        }
        break;
    case 't':
    case 'T':
        if ( g_state.playback == kTurntable )
        {
            g_state.playback = kStopped;
            glutIdleFunc( NULL );
        }
        else
        {
            g_state.playback = kTurntable;
            glutIdleFunc( turntableIdle );
        }
        break;
    case 'r':
    case 'R':
        RenderIt();
        break;
    case 'p':
        g_state.scene.pointSize =
            std::max( g_state.scene.pointSize-0.5f, 1.0f );
        glutPostRedisplay();
        break;
    case 'P':
        g_state.scene.pointSize =
            std::min( g_state.scene.pointSize+0.5f, 10.0f );
        glutPostRedisplay();
        break;
    case 'b':
    case 'B':
        bf = !bf;
        glLightModeli( GL_LIGHT_MODEL_TWO_SIDE, bf ? GL_FALSE : GL_TRUE );
        glutPostRedisplay();
        break;
        break;
    case '\t': // tab
        g_state.showHelp = !g_state.showHelp;
        glutPostRedisplay();
        break;
    case 27:
        exit(0);
        break;
    default:
        break;
    }
}
```

